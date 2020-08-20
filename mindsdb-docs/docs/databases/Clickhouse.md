# Machine Learning Models as Tables in ClickHouse

Now, you can train machine learning models straight from the database by using MindsDB and [ClickHouse](https://clickhouse.tech/).

![MindsDB-ClickHouse](/assets/clickhouse-mdb-diagram.png)


### Prerequisite

You will need MindsDB version >= 2.0.0 and ClickHouse installed.

### Configuration

!!! info "Default configuration"
    MindsDB will try to use the default configuration(hosts, ports, usernames) for each of the database integrations. If you want to extend that or you are
    using different parameters creata a new config.json file. 
The minimum required configuration inside config.json is:

```json
{
   "config_version": 1,
   "api": {
       "http": {
           "host": "0.0.0.0",
           "port": "47334"
       } ,
    "mysql": {
           "certificate_path": "/flows/config/cert.pem",
           "datasources": [],
           "host": "127.0.0.1",
           "log": {
               "console_level": "INFO",
               "file": "mysql.log",
               "file_level": "INFO",
               "folder": "logs/",
               "format": "%(asctime)s - %(levelname)s - %(message)s"
           },
           "password": "mysql pass",
           "port": "47335",
           "user": "mysql user"
       }
   },
   "debug": false,
   "integrations": {
       "default_clickhouse": {
           "enabled": true,
           "type": "clickhouse",
           "host": "localhost",
           "password": "pass",
           "port": 8123,
           "user": "default"
       }
   },
   "interface":{
       "datastore": {
           "enabled": false,
           "storage_dir": "/path/to/storage"
       }, 
    "mindsdb_native": {
           "enabled": true,
           "storage_dir": "/path/to/storage"
       }	
   }
}
```

* api -- This key is used for starting the MindsDB server by providing the host and port.
* mysql -- This key is used for database integrations that works through MySQL protocol. The required key's are username, password and MySQL host.
* integrations -- This key specifies the integration type in this case `default_clickhouse`. The required keys are user, host, password and port to the ClickHouse.
* interface -- This key is used by MindsDB and provides the path to the directory where MindsDB shall save some configuration and model files.

### Start MindsDB

```python
python3 -m mindsdb --api=mysql --config=config.json
```
The --api parameter specifies the type of API to use in this case mysql. 
The --config specifies the location of the configuration file. 

### Train new model

To train a new model, insert a new record inside the mindsdb.predictors table as:

```sql

INSERT INTO mindsdb.predictors(name, predict, select_data_query, training_options) VALUES ('airq_predictor', 'SO2', 'SELECT * FROM data.pollution_measurement', {"option": "value"});
```

* name (string) -- The name of the predictor.
* predict (string) --  The feature you want to predict, in this example SO2.
* select_data_query (string) -- The SELECT query that will ingest the data to train the model.
* training_options (JSON as string) -- optional value that contains additional training parameters. For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

### Query the model

To query the model and get the predictions SELECT the target variable, confidence and explanation for that prediction.

```sql
SELECT 
    SO2 AS predicted,
    SO2_confidence AS confidence,
    SO2_explain AS info
FROM airq_predictor
WHERE (NO2 = 0.005) AND (CO = 1.2) AND (PM10 = 5)
```
You should get a similar response from MindsDB as:

| price  | predicted | info   |
|----------------|------------|------|
| 0.001156540079952395 | 0.9869 | Check JSON bellow  |


```json
{
    "predicted_value": 0.001156540079952395,
    "confidence": 0.9869,
    "prediction_quality": "very confident",
    "confidence_interval": [0.003184904620383531, 0.013975553923630717],
    "important_missing_information": ["Station code", "Latitude", "O3"],
    "confidence_composition": {
        "CO": 0.006
    },
    "extra_insights": {
        "if_missing": [{
            "NO2": 0.007549311956155897
        }, {
            "CO": 0.005459383721227349
        }, {
            "PM10": 0.003870252306568623
        }]
    }
}
```

To get additional information about the integration check out [Machine Learning Models as Tables with ClickHouse](https://www.mindsdb.com/blog/machine-learning-models-as-tables) tutorial.