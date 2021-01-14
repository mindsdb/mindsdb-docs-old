# Connect to Snowflake Data Warehouse

Connecting MindsDB to Snowflake could be easly done with a few clicks. 

#### Connect to Snowflake

1. From the left navigation menu select Database Integration.
2. Click on the `ADD DATABASE` button. 
3. In the `Connect to Database` modal:
    1. Select Snowflake as Supported Database.
    2. Add the Database name.
    3. Add the Hostname.
    4. Add Port.
    5. Add Account.
    6. Add Warehouse.
    7. Add Schema.
    8. Add protocol.
    5. Add User.
    6. Add Password for the user.
    7. Click on `CONNECT`.

![Connect to Snowflake](/assets/data/snowflake.gif)

#### Create new Datasource

1. Click on the `NEW DATASOURCE` button.
2. In the `Datasource from DB integration` modal:
    1. Add Datasource Name.
    2. Add Database name.
    3. Add SELECT Query e.g (SELECT * FROM my_database)
    4. Click on `CREATE`.

![Create Snowflake Datasource](/assets/data/snowflake-ds.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully connected to Snowflake from MindsDB Scout. Next step is to train the [Machine Learning model](/model/train).