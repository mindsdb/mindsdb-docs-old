# Connect to PostgreSQL database

Connecting MindsDB to your PostgreSQL database could be done in two ways:

* Using MindsDB Graphical User Interface called [Scout](#mindsdb-scout).
* Using [psql client](#psql-client).

## Prerequisite

To connect to your PostgreSQL Server from MindsDB, you will need to install MySQL foreign data wrapper for PostgreSQL.

!!! Tip "How to install PostgreSQL foreign data wrapper"
    * Please check the mysql_fdw [documentation](https://github.com/EnterpriseDB/mysql_fdw#installation).
    * Stackoverflow [answers](https://stackoverflow.com/questions/24683035/setup-mysql-foreign-data-wrapper-in-postgresql).

## MindsDB Scout

Using MindsDB Scout, you can connect to the PostgreSQL database with a few clicks.

#### Connect to database

1. From the left navigation menu select Database Integration.
2. Click on the `ADD DATABASE` button. 
3. In the `Connect to Database` modal:
    1. Select PostgreSQL as Supported Database.
    2. Add the Database name.
    3. Add the Hostname.
    4. Add Port.
    5. Add PostgreSQL user.
    6. Add Password for PostgreSQL user.
    7. Click on `CONNECT`.


![Connect to PostgreSQL](/assets/data/postgresql.gif)

#### Create new Datasource

1. Click on the `NEW DATASOURCE` button.
2. In the `Datasource from DB integration` modal:
    1. Add Datasource Name.
    2. Add Database name.
    3. Add SELECT Query e.g (SELECT * FROM my_database)
    4. Click on `CREATE`.

![Create PostgreSQL Datasource](/assets/data/postgresql-ds.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected to PostgreSQL from MindsDB Scout. Next step is to train the [Machine Learning model](/model/train).

## PSQL client

Before using psql client to connect MindsDB and PostgreSQL Server you will need to add additional configuration before starting MindsDB Server. Create a new `config.json` file. Expand the example below to preview the configuration example.

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
        "default_postgres": {
            "database": "postgres",
            "publish": true,
            "host": "localhost",
            "password": "postgres",
            "port": 5432,
            "type": "postgres",
            "user": "postgres"
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
* [x] integrations['default_postgres'] -- This key specifies the integration type in this case `default_postgres`. The required keys are:
    * user(default postgres) - The Postgres user name.
    * host(default 127.0.0.1) - Connect to the PostgreSQL server on the given host. 
    * password - The password of the Postgres account. 
    * type - Integration type(mariadb, postgresql, mysql, clickhouse, mongodb).
    * port(default 5432) - The TCP/IP port number to use for the connection. 
    * publish(true|false) - Enable PostgreSQL integration.
* [ ] log['level'] -- The logging configuration(not required):
    * console - "INFO", "DEBUG", "ERROR".
    * file - Location of the log file.
* [x] storage_dir -- The directory where mindsdb will store models and configuration.

After creating the `config.json` file, you will need to start MindsDB and provide the path to the newly created `config.json` as:

```
python3 -m mindsdb --api=http,mysql --config=config.json
```
The `--api` parameter specifies the type of API to use in this case HTTP and MySQL. The `--config` specifies the location of the configuration file.

![Start MindsDB with config](/assets/data/psql-client.gif)


If MindsDB is succesfully connected to your PostgreSQL database, it will create a new schema `mindsdb` and new table `predictors`.
After starting the server, from your psql-client you can run `SELECT` query from it to make sure integration is succesfull.

```sql
SELECT * FROM mindsdb.predictors;
```

![SELECT from MindsDB predictors table](/assets/data/psql-select.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected MindsDB Server and PostgreSQL. Next step is to [train the Machine Learning model](/model/postgresql).