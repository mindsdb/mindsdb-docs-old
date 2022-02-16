
In MindsDB, the underlying automl models are based on Lightwood. This library generates model automatically based on the data and the problem definition, but the default configuration can be overridden.

# USING statement

The `USING ...` statement provides the option to configure a model to be trained.

## Syntax:

```sql
CREATE PREDICTOR [name_of_your _predictor]
FROM [name_of_your_integration]
    (SELECT * FROM your_database.your_data_table)
PREDICT [data_target_column]
USING 
[parameter] = ['parameter_value1']
;
```

# Parameters:

 THE ENCODER KEY 

Grants access to configure how each column is encoded; by default, the auto_ML will try to get the best match for the data. 
To learn more about how encoders work and their options, go [here](https://lightwood.io/encoder.html).

 THE MODEL KEY 

Allows you to specify what type of Machine Learning algorithm to learn from the encoder data. 

To learn more about all the model options, go [here](https://lightwood.io/mixer.html).
# Commmon Parameters Used

| Parameter   |      P       |  example  |
|----------|:-------------:|------:|
| 'use_gpu' |  boolean  | True |
| 'encoders.[column]' |  boolean  | True |
| 'encoders.[column]' |  boolean  | True |


# Actual example 

```sql
CREATE PREDICTOR home_rentals_model
FROM mariadb_integration
    (SELECT * FROM test_data.home_rentals)
PREDICT rental_price 
USING 
use_gpu = 'True'
,encoders.location.module='CategoricalAutoEncoder'
,encoders.rental_price.module = 'NumericEncoder'
;
```