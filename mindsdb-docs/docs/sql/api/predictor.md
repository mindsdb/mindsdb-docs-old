# Create Predictor Statement

The `CREATE PREDICTOR` statement is used to train new model. The basic syntax for training the model is:

* `CREATE PREDICTOR predictor_name` - where `predictor_name` is the name of the model.
* `FROM integration_name (select column_name FROM table_name)` - where `integration_name` is the name of the [datasource](/connect/#create-new-datasource), where `(select column_name FROM table_name)` is the SELECT statement for selecting the data. If you want to change the default name of the datasource you can use the alias `as ds_name`.
* `PREDICT column_name` - where `column_name` is the column name of the target variable. If you want to change the name of the target variable you can use the `as column_alias`.

```sql
CREATE PREDICTOR predictor_name
FROM integration_name 
(SELECT column_name, column_name2 FROM table_name) as ds_name
PREDICT column_name as column_alias;
```

### Example Data

The bellow database table contains prices of properties from a metropolitan area in the US.

{{ read_csv('https://raw.githubusercontent.com/mindsdb/mindsdb-examples/master/classics/home_rentals/dataset/train.csv', nrows=7) }}


### Create Predictor example
This example shows how you can train the Machine Learning Model called `house_price_model` to predict the rentals price from the above data.

```sql
CREATE PREDICTOR house_price_model
FROM integration_name (SELECT * FROM house_rentals_data) as rentals
PREDICT rental_price as price;
```

## ORDER BY keyword

The `ORDER BY` keyword is used to order the data by descending(DESC) or ascending(ASC) order. The default order will always be `ASC`

```sql
CREATE PREDICTOR predictor_name
FROM integration_name 
(SELECT column_name, column_name2 FROM table_name) as ds_name
PREDICT column_name as column_alias
ORDER BY column_name column_name2 ASC OR DESC;
```

### ORDER BY ASC example

The following example trains the new `house_price_model` model which predicts the `rental_price` and orders the data in ascending order by the number of days on the market.

```sql
CREATE PREDICTOR house_price_model
FROM integration_name (SELECT * FROM house_rentals_data) as rentals
PREDICT rental_price as price
ORDER BY days_on_market ASC;
```

### ORDER BY DESC example

The following example trains the new `house_price_model` model which predicts the `rental_price` and orders the data in descending order by the number of days on the market.

```sql
CREATE PREDICTOR house_price_model
FROM integration_name (SELECT * FROM house_rentals_data) as rentals
PREDICT rental_price as price
ORDER BY days_on_market DESC;
```

## GROUP BY statement

The `GROUP BY` statement is used to group the rows that contain the same values into one row.

```sql
CREATE PREDICTOR predictor_name
FROM integration_name 
(SELECT column_name, column_name2 FROM table_name) as ds_name
PREDICT column_name as column_alias
GROUP BY column_name
```

### GROUP BY example

The following example trains the new `house_price_model` model which predicts the `rental_price` and groups the data per location(good, great).

```sql
CREATE PREDICTOR house_price_model
FROM integration_name 
(SELECT * FROM house_rentals_data) as rentals
PREDICT rental_price as price
GROUP BY location;
```


## Time Series keywords

If you are training a timeseries model, MindsDB provides additional keywords. The `WINDOW` keyword specifies the number of rows to "look back" into when making a prediction after the rows are ordered by the order_by column and split into groups. Could be used to specify something like "Always use the previous 10 rows". The `HORIZON` keyword specifies the number of future predictions. 

```sql
CREATE PREDICTOR predictor_name
FROM integration_name 
(SELECT column_name, column_name2 FROM table_name) as ds_name
PREDICT column_name as column_alias
GROUP BY column_name
WINDOW 10
HORIZON 7;
```


## USING keyword

The `USING` keyword accepts arguments as a JSON format where additional arguments can be provided to the `CREATE PREDICTOR` statement as:

* `stop_train_in_x_seconds` - Stop model training after X seconds.
* `use_gpu` - Switch between training on CPU or GPU(true|false).
* `sample_margin_of_error` - The ammount of random sampling error in results (0 - 1)
* `ignore_columns` - Columns to be removed from the model training.

```sql
CREATE PREDICTOR predictor_name
FROM integration_name 
(SELECT column_name, column_name2 FROM table_name) as ds_name
PREDICT column_name as column_alias
USING {"ignore_columns": "column_name3"}
```

## USING example

The following example trains the new `house_price_model` model which predicts the `rental_price` and removes the number of bathrooms.

```sql
CREATE PREDICTOR house_price_model
FROM integration_name 
(SELECT * FROM house_rentals_data) as rentals
PREDICT rental_price as price
USING {"ignore_columns": "number_of_bathrooms"}
```