# Train a model from the MongoDB

![Train model from mongodb](/assets/databases/mongodb/mongo-mdb-code.png)


### Train new model

To train a new model, you will need to `insert()` a new document inside the mindsdb.predictors collection.

!!! question "How to create the mindsb.predictors table"
    Note that after connecting the [MindsDB and MongoDB Atlas](/datasources/mysql/#mysql-client), on
    start, the MindsDB server will automatically create the mindsdb database and add the predictors collection.


The object sent to the `insert()` for training the new model should contain:

* name (string) -- The name of the model.
* predict (string) --  The feature you want to predict. To predict multiple features, include a list of features.
* connection(string) -- The connection string for connecting to MongoDB Atlas. If you have used GUI to connect to MongoDB Atlas, that connection will be used.
* select_data_query (object) -- The object that contains info about getting the data to train the model.
    * database(string) - The name of the database
    * collection(string) - The name of the collection
    * find(dict) - The dict that selects the documents from the collection. Same as [db.collection.find({...})](https://docs.mongodb.com/manual/reference/method/db.collection.find/)
* training_options (dict) -- Optional value that contains additional training parameters. For a full list of parameters, check the [PredictorInterface](/PredictorInterface/#learn).

```sql
db.predictors.insert({
    'name': str,
    'predict': str | list of fields,
    'connection': str,  # optional
    'select_data_query':{
    'database': str,
    'collection': str,
    'find': dict  
    },
    'training_options': dict  # optional
})
```

### Train new model example

The following example shows you how to train a new model from a mongo client. The collection used for training the model is the [Telcom Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn) dataset.

```sql
db.predictors.insert({
    'name': 'churn',
    'predict': 'Churn',
    'select_data_query':{
        'database': 'test_data',
        'collection': 'customer_churn',
        'find': {} 
    }
})
```

![Train model from mongo shell](/assets/predictors/mongo/mongo-insert.gif)


This `INSERT` query will train a new model called `churn` that predicts the customer `Churn` value. 

#### Model training status

To check that the training finished successfully, you can `find()` the model status inside mindsdb.predictors collection e.g.:

```sql
db.predictors.find()
```

![Training model status](/assets/predictors/mongo/mongo-status.gif)

!!! Success "That's it :tada: :trophy:  :computer:"
    You have successfully trained a new model from a mongo shell. The next step is to get predictions by [querying the model](/model/query/mongodb).
