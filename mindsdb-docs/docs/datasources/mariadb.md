# Connect to MariaDB database

Connecting MindsDB to your MariaDB database could be done in two ways:

* Using MindsDB Graphical User Interface called [Scout](#mindsdb-scout).
* Using [SQL clients](#sql-clients).

## Prerequisite

To connect to MariaDB from MindsDB, you will need to install CONNECT Storage Engine.

!!! Tip "How to install CONNECT Storage Engine"
    * Please check the MariaDB [documentation](https://mariadb.com/kb/en/installing-the-connect-storage-engine/).
    * Read more about [CONNECT Storage Engine](https://mariadb.com/kb/en/introduction-to-the-connect-engine/).

## MindsDB Scout

Using MindsDB Scout, you can connect to the MariaDB database with a few clicks.

#### Connect to database

1. From the left navigation menu select Database Integration.
2. Click on the `ADD DATABASE` button. 
3. In the `Connect to Database` modal:
    1. Select MariaDB as Supported Database.
    2. Add the Database name.
    3. Add the Hostname.
    4. Add Port.
    5. Add MariaDB user.
    6. Add Password for MariaDB user.
    7. Click on `CONNECT`.


![Connect to MariaDB](/assets/data/mariadb.gif)

#### Create new Datasource

1. Click on the `NEW DATASOURCE` button.
2. In the `Datasource from DB integration` modal:
    1. Add Datasource Name.
    2. Add Database name.
    3. Add SELECT Query e.g (SELECT * FROM my_database)
    4. Click on `CREATE`.

![Create MariaDB Datasource](/assets/data/mariadb-ds.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected to MariaDB from MindsDB Scout. Next step is to train the [Machine Learning model](/model/train).

## MySQL client

Before using mysql-client to connect MindsDB and MariaDB you will need to add additional configuration before starting MindsDB Server. Create a new `config.json` file. Expand the example below to preview the configuration example.

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
        "default_mariadb": {
            "host": "localhost",
            "password": "pass",
            "port": 3306,
            "publish": true,
            "type": "mariadb",
            "user": "root"
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

* [x] api['http'] -- This key is used for starting the MindsDB HTTP server by providing:
    * host(default 127.0.0.1) - The mindsdb server address.
    * port(default 47334) - The mindsdb server port.
* [x] api['mysql'] -- This key is used for database integrations that work through MySQL protocol. The required keys are:
    * user(default root).
    * password(default empty).
    * host(default 127.0.0.1).
    * port(default 47335).
* [x] integrations['default_mariadb'] -- This key specifies the integration type in this case `default_mariadb`. The required keys are:
    * user(default root) - The MariaDB user name.
    * host(default 127.0.0.1) - Connect to the MariaDB server on the given host. 
    * password - The password of the MariaDB account. 
    * type - Integration type(mariadb, postgresql, mysql, clickhouse, mongodb).
    * port(default 3306) - The TCP/IP port number to use for the connection. 
    * publish(true|false) - Enable MariaDB integration.
* [ ] log['level'] -- The logging configuration(optional):
    * console - "INFO", "DEBUG", "ERROR".
    * file - Location of the log file.
* [x] storage_dir -- The directory where mindsdb will store models and configuration.

After creating the `config.json` file, you will need to start MindsDB and provide the path to the newly created `config.json` as:

```
python3 -m mindsdb --api=http,mysql --config=config.json
```

The `--api` parameter specifies the type of API to use in this case HTTP and MySQL. The `--config` specifies the location of the configuration file.

![Start MindsDB with config](/assets/data/start-config.gif)

If MindsDB is succesfully connected to your MariaDB database, it will create a new database `mindsdb` and new table `predictors`.
After starting the server, from your mariadb-client you can run `SELECT` query from it to make sure integration is succesfull.

```sql
SELECT * FROM mindsdb.predictors;
```

![SELECT from MindsDB predictors table](/assets/data/mariadb-select.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected MindsDB Server and MariaDB. Next step is to [train the Machine Learning model](/model/mariadb).