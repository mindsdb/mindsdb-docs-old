# How to train a model from MariaDB?

![MindsDB-MariaDB](/assets/databases/mdb-maria.png)

### How to train new model?

To train a new model, you will neeed to `INSERT` a new record inside the mindsdb.predictors table.

!!! question "How to create mindsb.predictors table"
    Note that after connecting [MindsDB and MariaDB](datasources/mariadb/#sql-clients), on
    start, MindsDB server will automaticly create the mindsdb database and add predictors table.

The `INSERT` query for training new model is quite simple e.g:

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query, training_options) 
VALUES('model_name', 'target_variable', 'SELECT * FROM table_name'); 
```
The values provided in `INSERT` query are:

* name (string) -- The name of the model.
* predict (string) --  The feature you want to predict. To predict multiple features include a comma separated string e.g 'consumption,income'.
* select_data_query (string) -- The SELECT query that will ingest the data to train the model.
* training_options (JSON as comma separated string) -- optional value that contains additional training parameters. For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

![Train model from mariadb client](/assets/predictors/mariadb-insert.gif)

### Train new model example

The following example shows you how to train new model from mariadb-client. The table used for training the model is same as [Used cars](https://www.kaggle.com/adityadesai13/used-car-dataset-ford-and-mercedes) dataset.

```sql
INSERT INTO
   mindsdb.predictors(name, predict, select_data_query) 
VALUES
   ('used_cars_model', 'price', 'SELECT * FROM data.used_cars_data');
```

### How to check model training status?

To check that the training successfully finished you can `SELECT` from mindsdb.predictors table and get the training status e.g:

```sql
SELECT * FROM mindsdb.predictors WHERE name='<model_name>';
```

![Training model status](/assets/predictors/mariadb-status.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully trained new model from MariaDB database. Next step is to get predictions by [querying the model](/model/query/mariadb).