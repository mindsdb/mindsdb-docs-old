# Connect to MongoDB database

Connecting MindsDB to MongoDB can be done in two ways:

* Using [MindsDB Studio](#mindsdb-studio).
* Using [Mongo clients](#mongo-shell).

The current integration works by accessing MongoDB through MindsDB MongoDB API as a new datasource.

![MindsDB-MongoDB](/assets/databases/mongodb/mongo-mdb-current.png)

The new version of MindsDB will allow direct integration inside MongoDB.

![MindsDB-MongoDB](/assets/databases/mongodb/mongo-mdb.png)


## MindsDB Studio

Using MindsDB Studio, you can connect to the MongoDB with a few clicks.

#### Connect to database

1. From the left navigation menu, select Database Integration.
2. Click on the `ADD DATABASE` button.
3. In the `Connect to Database` modal window:
    1. Select MongoDB as the Supported Database.
    2. Add Host (connection string)
    3. Add Port
    4. Add Username
    5. Add Password
    6. Click on `CONNECT`


![Connect to MongoDB](/assets/data/mongo/mongo.gif)

#### Create new dataset

1. Click on the `NEW DATASET` button.
2. In the `Datasource from DB integration` modal window:
    1. Add Datasource Name
    2. Add Database name
    3. Add Collection name
    3. Add find query to select documents from the collection(must be valid JSON format)
    4. Click on `CREATE`.

![Create Mongodb Datasource](/assets/data/mongo/mongo-ds.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully connected to MongoDB from MindsDB Studio. The next step is to train the [Machine Learning model](/model/train).


## Mongo shell


!!! Info "How to extend MindsDB configuration"
    Our suggestion is to always use [MindsDB Studio](/datasources/mariadb/#mindsdb-studio) to connect MindsDB to your database. If you still want to extend the configuration without using MindsDB Studio follow the steps below.

Before using the mongo client to connect MindsDB and MongoDB, you will need to add additional configuration before starting MindsDB Server. Create a new `config.json` file. Expand the example below to preview the configuration example.

<details class="success">
   <summary> Configuration example</summary> 
```json
{
    "api": {
        "http": {
            "host": "127.0.0.1",
            "port": "47334"
        },
        "mysql": {}
        "mongodb": {
            "host": "127.0.0.1",
            "port": "47336"
        }
    },
    "config_version": "1.4",
    "debug": true,
    "integrations": {},
    "storage_dir": "/mindsdb_storage"
}
```       
</details>

All of the options that should be added to the `config.json` file are:

* [x] api['http'] -- This key is used for starting the MindsDB HTTP API by providing:
    * host(default 127.0.0.1) - MindsDB server address.
    * port(default 47334) - MindsDB server port.
* [x] api['mongodb'] -- This key is used for starting MindsDB Mongo API by providing:
    * host(default 127.0.0.1) - MindsDB Mongo API address.
    * port(default 47335) - MindsDB Mongo API port.
* [ ] api['mysql] -- This key is used for starting MindsDB MySQL API. Leave it empty if you work only with MongoDB.
* [ ] config_version(latest 1.4) - The version of config.json file. 
* [ ] debug(true|false)
* [ ] integrations[''] -- This key specifies the integration options with other SQL databases. Leave it empty if you work only with MongoDB. 
* [ ] log['level'] -- The logging configuration(optional):
    * console - "INFO", "DEBUG", "ERROR".
    * file - Location of the log file.
* [x] storage_dir -- The directory where mindsDB will store models and configuration files.

After creating the `config.json` file, you will need to start MindsDB and provide the path to the newly created `config.json`:

```
python3 -m mindsdb --api=http,mongodb --config=config.json
```

The `--api` parameter specifies the type of API to use -- in this case HTTP and Mongo. The `--config` parameter specifies the location of the configuration file.

![Start MindsDB with config](/assets/data/mongo/start-mongo.gif)


### Connect to MongoDB API

To connect to mindsdb's MongoDB API, use the `host` that you have specified inside the `api['mongodb']` key e.g:

```
mongo --host 127.0.0.1
```

To make sure everything works, you should be able to see the predictors collection.

```
use mindsdb
show collections
```



![find mindsdb predictors collection](/assets/data/mongo/find-predictors.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully connected MindsDB Server and MongoDB. The next step is to [train the Machine Learning model](/model/mongodb).

