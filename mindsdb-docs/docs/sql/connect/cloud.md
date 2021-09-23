# MindsDB Cloud as a SQL Database

MindsDB Cloud provides a powerful MySQL API that allows cloud users to connect to it using the [MySQL Command-Line Client](https://dev.mysql.com/doc/refman/8.0/en/mysql.html) or [DBeaver](https://dbeaver.io/). The first step to connect is to use the MindsDB Cloud user. If you haven't signup to the MindsDB Cloud follow the steps explained [here](/deployment/cloud).

Open mysql client and run:

```
mysql -h cloud-mysql.mindsdb.com --port 3306 -u cloudusername@mail.com -p
```
The required parameters are:

* -h: Host name of mindsdbs mysql api (cloud-mysql.mindsdb.com)	
* --port: TCP/IP port number for connection(3306)	
* -u: MindsDB Cloud username
* -p:  MindsDB Cloud password

![Connect](/assets/sql/mysql-client.gif)

Or, if you are using another database manager interface make sure to select Driver for MySQL 8 and later.

![Connect](/assets/sql/connectcloud.png)

## MindsDB Database

On the start mindsdb database will contain 2 tables `predictors` and `commands`. 

![Connect](/assets/sql/show.png)

All of the new trained machine learning models will be vissible as a new record inside the `predictors` table. The `predictors` columns contains information about each model as:

* name - The name of the model.
* status - Training stauts(training, complete, error).
* accuracy - The model accuracy.
* predict - The name of the target varaibale.
* select_data_query - SQL select query to create the datasource.
* external_datasource - Name of the pre existing datasource created from GUI.
* training options - Additional training parameters. The full list can be found at [PredictorInterface docs](/PredictorInterface/#learn).


!!! tip "Whitelist MindsDB Cloud IP address"
    If you need to whitelist MindsDB Cloud IP address to have access to your database, reach out to MindsDB team so we share the Cloud static IP with you.