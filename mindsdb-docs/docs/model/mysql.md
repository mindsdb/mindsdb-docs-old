# Train a model from MySQL database

![MindsDB-MySQL](/assets/databases/mdb-mysql.png)

### Train new model

To train a new model, you will neeed to `INSERT` a new record inside the mindsdb.predictors table.

!!! question "How to create mindsb.predictors table"
    Note that after connecting [MindsDB and MySQL servers](datasources/mysql/#mysql-client), on
    start, MindsDB server will automaticly create the mindsdb database and add predictors table.

The `INSERT` query for training new model is quite simple e.g:

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query)
VALUES('model_name', 'target_variable', 'SELECT * FROM table_name'); 
```

The values provided in `INSERT` query are:

* name (string) -- The name of the model.
* predict (string) --  The feature you want to predict. To predict multiple features include a comma separated string e.g 'feature1,feature2'.
* select_data_query (string) -- The SELECT query that will ingest the data to train the model.
* training_options (JSON as comma separated string) -- optional value that contains additional training parameters. For a full list of the parameters check the [PredictorInterface](/PredictorInterface/#learn).

![Train model from mysql client](/assets/predictors/mysql-insert.gif)

### Train new model example

The following example shows you how to train new model from mysql-client. The table used for training the model is same as [Us consumption](https://github.com/robjhyndman/fpp2-package/blob/15916e4fe827d1b3dcf82785a4ace80107af5ddd/data-raw/usconsumption.csv) dataset.

```sql
INSERT INTO mindsdb.predictors(name, predict, select_data_query,training_options) VALUES ('airq_predictor', 'SO2', 'SELECT * FROM default.pollution_measurement', '{"timeseries_settings":{"order_by": ["Measurement date"], "window":20}}');
```

This `INSERT` query will train a new model called `airq_predictor` that predicts the `SO2` value. Since, this is a timeseries data the `timeseries_settings` will order data by `t` column and will set the window for rows to "look back" when making a prediction.

#### Model training status

To check that the training successfully finished you can `SELECT` from mindsdb.predictors table and get the training status e.g:

```sql
SELECT * FROM mindsdb.predictors WHERE name='<model_name>';
```

![Training model status](/assets/predictors/mysql-status.gif)

!!! Success "That's all :tada: :trophy:  :computer:"
    You have succesfully trained new model from MySQL database. Next step is to get predictions by [querying the model](/query/mysql).