# Connect to MongoDB database

Currently, the MongoDB integration works only with MongoDB Atlas the cloud-hosted MongoDB service. Connecting MindsDB to MongoDB Atlas can be done in two ways:

* Using [MindsDB Studio](#mindsdb-studio).
* Using [Mongo shell](#mongo-shell).

## MindsDB Studio

Using MindsDB Studio, you can connect to the MongoDB Atlas with a few clicks.

#### Connect to database

1. From the left navigation menu, select Database Integration.
2. Click on the `ADD DATABASE` button.
3. In the `Connect to Database` modal window:
    1. Select MongoDB as the Supported Database.
    2. Add Host
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
    3. Add find query to select documents from the collection
    4. Click on `CREATE`.

![Create Mongodb Datasource](/assets/data/mongo/mongo-ds.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully connected to MongoDB Atlas from MindsDB Studio. The next step is to train the [Machine Learning model](/model/train).