# Connect to ClickHouse database

Connecting MindsDB to your ClickHouse database could be done in two ways:

* Using MindsDB Graphical User Interface called [Scout](#mindsdb-scout).
* Using [clickhouse client](#clickhouse-client).

## MindsDB Scout

Using MindsDB Scout, you can connect to the ClickHouse database with a few clicks.

#### Connect to database

1. From the left navigation menu select Database Integration.
2. Click on the `ADD DATABASE` button. 
3. In the `Connect to Database` modal:
    1. Select ClickHouse as Supported Database.
    2. Add the Database name.
    3. Add the Hostname.
    4. Add Port.
    5. Add ClickHouse user.
    6. Add Password for ClickHouse user.
    7. Click on `CONNECT`.


![Connect to ClickHouse](/assets/data/clickhouse.gif)

#### Create new Datasource

1. Click on the `NEW DATASOURCE` button.
2. In the `Datasource from DB integration` modal:
    1. Add Datasource Name.
    2. Add Database name.
    3. Add SELECT Query e.g (SELECT * FROM my_database)
    4. Click on `CREATE`.

![Create ClickHouse Datasource](/assets/data/clickhouse-ds.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected to ClickHouse from MindsDB Scout. Next step is to train the [Machine Learning model](/model/train).

## ClickHouse client

Before using clickhouse client to connect MindsDB and ClickHouse Server you will need to add additional configuration before starting MindsDB Server. Create a new `config.json` file. Expand the example below to preview the configuration example.

<details class="success">
    <summary> Configuration example</summary>  
```json
{
    "api": {
        "http": {
            "host": "127.0.0.1",
            "port": "47334"
        },
        "mysql": {
            "host": "127.0.0.1",
            "password": "",
            "port": "47335",
            "user": "root"
        }
    },
    "config_version": "1.4",
    "debug": true,
    "integrations": {
        "default_clickhouse": {
            "database": "default",
            "published": true,
            "type": "clickhouse",
            "host": "localhost",
            "password": "pass",
            "port": 8123,
            "user": "default"
        }
    },
    "log": {
        "level": {
            "console": "DEBUG",
            "file": "INFO"
        }
    },
    "storage_dir": "/storage"
}
```        
</details> 

All of the options that should be added to the `config.json` file are:

The avaiable configuration options are:

* [x] api['http] -- This key is used for starting the MindsDB http server by providing:
    * host(default 127.0.0.1) - The mindsdb server address.
    * port(default 47334) - The mindsdb server port.
* [x] api['mysql'] -- This key is used for database integrations that works through MySQL protocol. The required keys are:
    * user(default root).
    * password(default empty).
    * host(default 127.0.0.1).
    * port(default 47335).
* [x] integrations['default_clickhouse'] -- This key specifies the integration type in this case `default_clickhouse`. The required keys are:
    * user(default is default user) - The ClickHouse user name.
    * host(default 127.0.0.1) - Connect to the ClickHouse server on the given host. 
    * password - The password of the ClickHouse user. 
    * type - Integration type(mariadb, postgresql, mysql, clickhouse, mongodb).
    * port(default 8123) - The TCP/IP port number to use for the connection. 
    * publish(true|false) - Enable ClickHouse integration.
* [ ] log['level'] -- The logging configuration(not required):
    * console - "INFO", "DEBUG", "ERROR".
    * file - Location of the log file.
* [x] storage_dir -- The directory where mindsdb will store models and configuration.

After creating the `config.json` file, you will need to start MindsDB and provide the path to the newly created `config.json` as:

```
python3 -m mindsdb --api=http,mysql --config=config.json
```
The `--api` parameter specifies the type of API to use in this case HTTP and MySQL. The `--config` specifies the location of the configuration file.

![Start MindsDB with config](/assets/data/clickhouse-client.gif)


If MindsDB is succesfully connected to your ClickHouse database, it will create a new database `mindsdb` and new table `predictors`.
After starting the server, from your clickhouse-client you can run `SELECT` query from it to make sure integration is succesfull.

```sql
SELECT * FROM mindsdb.predictors;
```

![SELECT from MindsDB predictors table](/assets/data/clickhouse-select.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected MindsDB Server and ClickHouse. Next step is to [train the Machine Learning model](/model/clickhouse).