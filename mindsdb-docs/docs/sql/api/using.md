# USE statement

The `USING ...` statement provides an option to provide extra details to configure a model to be trained.

## Structure:

```sql

CREATE PREDICTOR {name_of_your _predictor}
FROM name_of_your_integration
    (SELECT * FROM your_database.your_data_table)
PREDICT data_column
USING 
parameter = 'parameter_value1'
,encoders.columnn.module='EncoderParameter'
;
```

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

# Parameters:
| parameter   |      Type       |  example  |
|----------|:-------------:|------:|
| 'use_gpu' |  boolean  | True |