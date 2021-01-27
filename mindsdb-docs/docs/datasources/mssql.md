# Connect to Microsoft SQL Server

Connecting MindsDB to your Microsoft SQL Server can be done in two ways:

* Using [MindsDB Studio](#mindsdb-studio).
* Using [mssql client](#) WIP.

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