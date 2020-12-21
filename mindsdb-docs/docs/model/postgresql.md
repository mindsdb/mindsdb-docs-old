# Train a model from PostgreSQL database

![MindsDB-MySQL](/assets/databases/mdb-postgres.png)

### Train new model

To train a new model, you will neeed to `INSERT` a new record inside the mindsdb.predictors table.

!!! question "How to create mindsb schema and tables"
    Note that after connecting [MindsDB and PostgreSQL](/datasources/postgresql/#psql-client), on start, MindsDB server will automaticly create the mindsdb schema and add predictors table.

The `INSERT` query for training new model is quite simple e.g:

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query, training_options) VALUES ('model_name', 'target_variable', 'SELECT * FROM table_name', '{"additional_training_params:value"}');
```
The values provided in `INSERT` query are:

* name (string) -- The name of the model.
* predict (string) --  The feature you want to predict. To predict multiple features include a comma separated string e.g 'consumption,income'.
* select_data_query (string) -- The SELECT query that will ingest the data to train the model.
* training_options (JSON as comma separated string) -- optional value that contains additional training parameters. For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

![Train model from psql client](/assets/predictors/postgresql-insert.gif)

### Train new model example

The following example shows you how to train new model from psql-client. The table used for training the model is same as [Airline Passenger sattisfaction](https://www.kaggle.com/teejmahal20/airline-passenger-satisfaction) dataset.

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query) VALUES('airline_survey_model', 'satisfaction', 'SELECT * FROM airline_passenger_satisfaction');
```


### Model training status

To check that the training successfully finished you can `SELECT` from mindsdb.predictors table and get the training status e.g:

```sql
SELECT * FROM mindsdb.predictors WHERE name='<model_name>';
```

![Training model status](/assets/predictors/postgresql-status.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully trained new model from PostgreSQL database. Next step is to get predictions by [querying the model](/model/query/postgresql/).