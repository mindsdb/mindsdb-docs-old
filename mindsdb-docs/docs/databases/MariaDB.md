# Machine Learning Models as Tables in MariaDB

Now, you can train machine learning models straight from the database by using MindsDB and [MariaDB](https://mariadb.org/).

![MindsDB-ClickHouse](/assets/clickhouse-mdb-diagram.png)

### Prerequisite

You will need MindsDB version >= 2.0.0 and MariaDB installed.

### Configuration

!!! info "Default configuration"
    MindsDB will try to use the default configuration(hosts, ports, usernames) for each of the database integrations. If you want to extend that or you are
    using different parameters creata a new config.json file. 
The minimum required configuration inside config.json is:

```json
{
   "api": {
       "http": {
           "host": "0.0.0.0",
           "port": "47334"
       },
       "mysql": {
           "certificate_path": "path/to/cert", 
           "host": "127.0.0.1",
           "log": {
               "console_level": "INFO",
               "file": "mysql.log",
               "file_level": "INFO",
               "folder": "logs/",
               "format": "%(asctime)s - %(levelname)s - %(message)s"
           },
           "password": "root",
           "port": "47335",
           "user": "pass"
       }
   },
   "config_version": "1.1",
   "debug": true,
   "integrations": {
       "default_mariadb": {
           "enabled": true,
           "host": "localhost",
           "password": "password",
           "port": 3306,
           "type": "mariadb",
           "user": "root"
       }
   },
   "interface": {
       "datastore": {
           "enabled": true,
           "storage_dir": "/path/to/storage"
       },
       "mindsdb_native":{
           "enabled": true,
           "storage_dir": "/path/to/storage"
       }
   }
}
```

* api -- This key is used for starting the MindsDB server by providing the host and port.
* mysql -- This key is used for database integrations that works through MySQL protocol. The required keys are username, password and MySQL host.
* integrations -- This key specifies the integration type in this case `default_mariadb`. The required keys are user, host, password and port to connect to the MariaDB.
* interface -- This key is used by MindsDB and provides the path to the directory where MindsDB shall save some configuration and model files.

Also you need to install the CONNECT Storage Engine to access external local data. Checkout [MariaDB docs](https://mariadb.com/kb/en/installing-the-connect-storage-engine/) on how to do that.


### Start MindsDB

```python
python3 -m mindsdb --api=mysql --config=config.json
```
The --api parameter specifies the type of API to use in this case mysql. 
The --config specifies the location of the configuration file. 

### Train new model

To train a new model, insert a new record inside the mindsdb.predictors table as:

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query, training_options) VALUES ('used_cars_model', 'price', 'SELECT * FROM test.UsedCarsData', {"option": "value"});
```

* name (string) -- The name of the predictor.
* predict (string) --  The feature you want to predict, in this example SO2.
* select_data_query (string) -- The SELECT query that will ingest the data to train the model.
* training_options (JSON as string) -- optional value that contains additional training parameters. For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

### Query the model

To query the model and get the predictions SELECT the target variable, confidence and explanation for that prediction.

```sql
SELECT price AS predicted, price_confidence AS confidence, price_explain AS info FROM mindsdb.used_cars_model WHERE model="A6" AND mileage=36203 AND transmission="Automatic"  AND fuelType="Diesel" AND mpg="64.2" AND engineSize=2 AND year=2016 AND tax=20;
```
You should get a similar response from MindsDB as:

| price  | predicted | info   |
|----------------|------------|------|
| 13111 | 0.9921 | Check JSON bellow  |

```json

{
    "predicted_value": 13111,
    "confidence": 0.9921,
    "prediction_quality": "very confident",
    "confidence_interval": [10792, 32749],
    "important_missing_information": [],
    "confidence_composition": {
        "Model": 0.009,
        "year": 0.013
    },
    "extra_insights": {
        "if_missing": [{
            "Model": 12962
        }, {
            "year": 12137
        }, {
            "transmission": 2136
        }, {
            "mileage": 22706
        }, {
            "fuelType": 7134
        }, {
            "tax": 13210
        }, {
            "mpg": 27409
        }, {
            "engineSize": 13111
        }]
    }
}

```

To get additional information about the integration check out [Machine Learning Models as Tables with MariaDB]() tutorial.