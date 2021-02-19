# Connect to Microsoft SQL Server

Connecting MindsDB to your Microsoft SQL Server can be done in two ways:

* Using [MindsDB Studio](#mindsdb-studio).
* Using [mssql client](#mssql-client).

!!! Warning "Install MindsDB"
    If you want to use Microsoft SQL Server integration, you will need to install MindsDB with pip or from source. The reason for this is that you will need to install additonal requirements:
    ```
    pip3 install 'pymssql >= 2.1.4' --upgrade
    ```

## Prerequisite

To connect to your Microsoft SQL Server from MindsDB, you will need to install Microsoft OLEDB Provider driver.

!!! Tip "How to install "
    * Please check that your MSSQL instance have [MSDASQL installed](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/open-the-odbc-data-source-administrator?view=sql-server-ver15).
    * If not, download  driver from [here](https://dev.mysql.com/downloads/connector/odbc/).
    * [Microsoft OLE DB Provider for ODBC Overview](https://docs.microsoft.com/en-us/sql/ado/guide/appendixes/microsoft-ole-db-provider-for-odbc?view=sql-server-ver15).

## MindsDB Studio

Using MindsDB Studio, you can connect to the Microsoft SQL Server with a few clicks.

#### Connect to database

1. From the left navigation menu, select Database Integration.
2. Click on the `ADD DATABASE` button.
3. In the `Connect to Database` modal window:
    1. Select `Microsoft SQL Server` as the Supported Database.
    2. Add the Database name.
    3. Add the Hostname.
    4. Add Port.
    5. Add SQL Server user.
    6. Add Password for SQL Server user.
    7. Click on `CONNECT`.


![Connect to MSSQL](/assets/data/mssql.gif)

#### Create new Datasource

1. Click on the `NEW DATASOURCE` button.
2. In the `Datasource from DB integration` modal window:
    1. Add Datasource Name.
    2. Add Database name.
    3. Add SELECT Query (e.g. SELECT * FROM my_database)
    4. Click on `CREATE`.

![Create MSSQL Datasource](/assets/data/mssql-ds.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully connected to Microsoft SQL Server from MindsDB Studio. The next step is to train the [Machine Learning model](/model/train).

## MSSQL client

!!! Info "How to extend MindsDB configuration"
    Our suggestion is to always use [MindsDB Studio](/datasources/mssql/#mindsdb-studio) to connect MindsDB to your database. If you still want to extend the configuration without using MindsDB Studio follow the steps below.

Before using mssql-cli or any SQL client to connect MindsDB and Microsoft SQL Server, you will need to add additional configuration before starting MindsDB Server. Create a new `config.json` file. Expand the example below to preview the configuration example.

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
           "database": "mindsdb",
           "password": "",
           "port": "47335",
           "ssl": true,
           "user": "root"
       }
   },
   "config_version": "1.4",
   "debug": true,
   "integrations": {
       "default_mariadb": {
           "host": "localhost",
           "password": "pass",
           "port": 1433,
           "publish": true,
           "type": "mssql",
           "user": "sa"
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
    * host(default 127.0.0.1) - The mindsDB server address.
    * port(default 47334) - The mindsDB server port.
* [x] api['mysql'] -- This key is used for database integrations that work through MySQL protocol. The required keys are:
    * user(default root).
    * password(default empty).
    * database - The name of the server that mindsdb will start.
    * ssl(default true) -- Use SSL true/false.
    * host(default 127.0.0.1).
    * port(default 47335).
* [x] integrations['default_mssql'] -- This key specifies the integration type, in this case `default_mssql`. The required keys are:
    * user(default sa) - The Microsoft SQL Server user name.
    * host(default 127.0.0.1) - Connect to the Microsoft SQL Server on the given host.
    * password - The password of the Microsoft SQL Server user.
    * type - Integration type(mariadb, postgresql, mysql, clickhouse, mongodb).
    * port(default 1433) - The TCP/IP port number to use for the connection.
    * publish(true|false) - Enable Microsoft SQL Server integration.
* [ ] log['level'] -- The logging configuration(optional):
    * console - "INFO", "DEBUG", "ERROR".
    * file - Location of the log file.
* [x] storage_dir -- The directory where mindsDB will store models and configuration.

After creating the `config.json` file, you will need to start MindsDB and provide the path to the newly created `config.json`:

```
python3 -m mindsdb --api=http,mysql --config=config.json
```

The `--api` parameter specifies the type of API to use -- in this case HTTP and MySQL. The `--config` parameter specifies the location of the configuration file.

![Start MindsDB with config](/assets/data/start-config.gif)

After starting the server, you can run a `SELECT` query from your SQL client to make sure integration has been successful. Please make sure to use `exec` or `openquery` as the examples bellow.

```sql
exec ('SELECT * FROM mindsdb.predictors') AT mindsdb_db;
```
Or, `openquery`:
```sql
select * from openquery(mindsdb, 'select * from mindsdb.predictors'); 
```
>Note: `mindsdb` is the name of the api['mysql]['database'] key from config.json. The default name is `mindsdb`.

![SELECT from MindsDB predictors table](/assets/data/mssql-select.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully connected MindsDB Server and Microsoft SQL Server. The next step is to [train the Machine Learning model](/model/mssql).