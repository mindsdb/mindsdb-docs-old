# AI-Tables in MySQL

Anyone that has dealt with Machine Learning understands that data is a fundamental ingredient to it. Given that a great deal of the world’s organized data already exists inside databases, doesn't it make sense to bring machine learning capabilities straight to the database itself? Bringing Machine Learning to those who know their data best can significantly augment the capacity to solve important problems.
To do so, we have developed a concept called AI-Tables.

## What is AI Tables

AI-Tables differ from normal tables in that they can generate predictions upon being queried and returning such predictions as if it was data that existed in the table. Simply put, an AI-Table allows you to use machine learning models as if they were normal database tables, in something that in plain SQL looks like this:

```sql
SELECT <predicted_variable> FROM <ML_model> WHERE <conditions>
```

Now, in this tutorial you will get a step-by-step instructions on how to enable AI-Tables in your database and how to build, train and query a Machine Learning model only by using SQL statements!

## How to install MySQL?

If you don’t have MySQL installed you can download the installers for various platforms from the official documentation.

## Example dataset

In this tutorial, we will use the [Metro Interstate Traffic Volume Data Set
](https://archive.ics.uci.edu/ml/datasets/Metro+Interstate+Traffic+Volume#). If you have other datasets in your MySQL database please skip this section. This dataset contains hourly traffic volume for station 301. Hourly weather features and holidays included for impacts on traffic volume.

#### Import dataset to MySQL
The first thing we need to do is to import the dataset in MySQL. Create a new table called metro_trafic:

```sql
-- test.metro_trafic definition

CREATE TABLE `metro_trafic` (
  `holiday` varchar(100) DEFAULT NULL,
  `temp` decimal(10,0) DEFAULT NULL,
  `rain_1h` decimal(10,0) DEFAULT NULL,
  `snow_1h` decimal(10,0) DEFAULT NULL,
  `clouds_all` decimal(10,0) DEFAULT NULL,
  `weather_main` varchar(100) DEFAULT NULL,
  `weather_description` varchar(100) DEFAULT NULL,
  `date_time` varchar(100) DEFAULT NULL,
  `traffic_volume` decimal(10,0) DEFAULT NULL
) ENGINE=InnoDB 
DEFAULT CHARSET=utf8mb4 
COLLATE=utf8mb4_0900_ai_ci;
```

Next, we need the import data inside the table. There are few options to do that:


Using the Load Data statement:
```
LOAD DATA LOCAL INFILE 'data.csv' INTO metro_trafic FIELDS TERMINATED BY ',' LINES TERMINATED BY '\r\n';
``` 
Using MySQL import:

```
mysqlimport --local --fields-terminated-by="," used_cars_data data.csv
```
Using pgAdmin, DBeaver or another SQL client just use the import from CSV file option from the navigation menu. 

Let’s Select some data from metro_trafic table to check that the data was successfully imported to MySQL:

```sql
SELECT * FROM metro_trafic LIMIT 10;
```

![SELECT FROM us_consumption](/assets/tutorials/aitables-mysql/select_table.png)

## Add Configuration

As a prerequisite for using MySQL we need to enable the Federated Storage engine. Check out official [MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/federated-storage-engine.html) to see how you can do that.
The last step is to create the MindsDB’s configuration file. MindsDB will try to use the default configuration options like host, port, username for the MySQL. In case you want to extend them or change the default values you need to add a config.json file. Create a new file config.json and include the following information:

```json
{
   "api": {
       "http": {
           "host": "0.0.0.0",
           "port": "47334"
       },
       "mysql": {
           "host": "127.0.0.1",
           "password": "",
           "port": "47335",
           "user": "root"
       }
   },
   "config_version": "1.3",
   "debug": true,
   "integrations": {
              "default_mysql": {
           "enabled": true,
           "host": "localhost",
           "password": "root",
           "port": 3307,
           "type": "mysql",
           "user": "root"
       }
   },
   "log": {
       "level": {
           "console": "DEBUG",
           "file": "INFO"
       }
   },
   "storage_dir": "storage/"
}
```

The values provided in the configuration file are:

* api['http’] -- This key is used for starting the MindsDB HTTP server by providing:
host(default 127.0.0.1) - The mindsdb server address.
* port(default 47334) - The mindsdb server port.
* api['mysql'] -- This key is used for database integrations that work through MySQL protocol. The required keys are:
   * user(default root).
   * password(default empty).
   * host(default 127.0.0.1).
   * port(default 47335).
* integrations[default_mysql] -- This key specifies the integration type in this case default_mysql. The required keys are:
   * user(default root) - The MySQL user name.
   * host(default localhost) - Connect to the MySQL server on the given host.
   * password - The password of the MySQL account.
   * type - Integration type(mariadb, postgresql, mysql, clickhouse, mongodb).
   * port(default 5432) - The TCP/IP port number to use for the connection.
* log['level'] -- The logging configuration(not required):
console - "INFO", "DEBUG", ”WARNING”,  "ERROR".
* file - Log level to save in the log file.
* storage_dir -- The directory where mindsdb will store models and configuration.
Now, we have successfully set up all of the requirements for AI Tables in MySQL.

### AutoML with AI Tables in MySQL
Let’s start the MindsDB server:

```
python3 -m mindsdb --api=mysql --config=config.json
```

The arguments sent to MindsDB are:
* --api - That tells MindsDB which API should be started (HTTP or MySQL).
* --config - The path to the configuration file that we have created.
If everything works as expected you should see the following message:

![MindsDB Started](/assets/tutorials/aitables-postgresql/mindsdb_started.png)


Upon successful setup, MindsDB should create a new database called mindsdb.

![MindsDB Schema](/assets/tutorials/aitables-mysql/list_tables.png)


In the mindsdb database, two new tables should be created called commands and predictors. The mindsdb.predictors table is the table where MindsDB will keep information about trained and in training models.

### Train new Machine Learning Model

Training the machine learning model using MindsDB is quite simple. It can be done by executing the INSERT query inside the mindsdb.predictors table. In our example we want to predict the consumption from the us_consumption table, so let’s run the INSERT query as:

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query, training_options) VALUES ('metro_traffic_model', 'traffic_volume', 'SELECT * FROM test.metro_trafic', '{"timeseries_settings":{"order_by": ["date_time"], "window":20}}');
```

This query will create a new model called 'metro_traffic_model', and a new table 'metro_traffic_model' inside mindsdb database. The required columns(parameters) added in the INSERT for training the predictor are:
* name (string) - the name of the predictor.
* predict (string) -  the feature you want to predict, in this example it will be satisfaction.
* select_data_query (string) - the SELECT query that will get the data from MySQL.
* training_options (dictionary) - optional value that contains additional training parameters. Because this is a timeseries data we have included order_by to order the data based on that column and window which is the number of columns to loop back.  For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

To check that the training successfully finished we can SELECT from mindsdb.predictors table and get the status:

```sql
SELECT * FROM mindsdb.predictors WHERE name='metro_traffic_model';
```

![Status](/assets/tutorials/aitables-mysql/select_status.png)

The status complete means that training successfully finished. Now, let’s query the model. The trained model behaves like an AI Table and can be queried as it is a standard database table. To get the prediction we need to execute a `SELECT` query and in the `WHERE` clause include the when_data as an JSON string that includes features values such as date_time, weather, temperature, holiday etc.

```sql
mysql> select * from mindsdb.metro_traffic_model where when_data='{"temp": "288","snow_1h":0, "date_time": "2012-10-02", "holiday":"Columbus Day"}';
```

In a second we should get the prediction back from MindsDB. So, MindsDB thinks that the value for traffic_volume value is 4524 with pretty much big confidence 99%.

Information in JSON format in the explain column:

```json
{
   "predicted_value": 4524,
   "confidence": 0.987,
   "prediction_quality": "very confident",
   "important_missing_information": ["weather_main"],
   "confidence_composition": {
       "age": 0.935
   },
   "extra_insights": {
       "if_missing": [{
           "temp": "3908"
       }, {
           "holiday": "4324"
       }, {
           "snow_1h": "4420"
       }]
   }
}
```

The confidence_interval shows a possible range of values where consumption lies in. The important_missing_information shows the list of features that MindsDB things are quite important for better prediction, in this case, the “weather_main”. The extra_insights contains a list of rows that we have included in the WHERE clause and show the traffic_volume value if some of those were missing.

Congratulations, you have successfully trained and queried the Machine Learning Model only by using SQL Statements. Note that even if we used MySQL, you can still query the same model from the other databases too.


