# How to query the model from MariaDB database?

This section assumes that you have trained new model using [mariadb](model/mariadb/) or [MindsDB Scout](model/train/). To query the model, you will neeed to `SELECT` from the model table as:

```sql
SELECT
   <target_variable> AS predicted,
   <target_variable_confidence> AS confidence,
   <target_variable_explain> AS info 
FROM
   mindsdb.<model_name>
WHERE 
   <feature_one> AND <feature_two>
```

!!! question "Query the model from other databases"
    Note that even if you have trained the model from the MariaDB database, you will be able to
    query it from other databases too.

## Query example

The following example shows you how to train new model from mariadb-client. The table used for training the model is same as [Used cars](https://www.kaggle.com/adityadesai13/used-car-dataset-ford-and-mercedes) dataset. MindsDB will predict the `price` based on the values added in `WHERE` clause.

```sql
SELECT
   price AS predicted,
   price_confidence AS confidence,
   price_explain AS info 
FROM
   mindsdb.used_cars_model 
WHERE
   model = "A6" 
   AND mileage = 36203 
   AND transmission = "Automatic" 
   AND fuelType = "Diesel" 
   AND mpg = "64.2" 
   AND engineSize = 2 
   AND year = 2016 
   AND tax = 20;
```

You should get a similar response from MindsDB as:

| price  | confidence | info   |
|----------------|------------|------|
| 16117 | 0.98 | Check JSON bellow  |

```json
info: {
    "predicted_value": 16117.627834024992,
    "confidence": 0.98,
    "prediction_quality": "very confident",
    "confidence_interval": [10737.135673357996, 21498.119994691988],
    "important_missing_information": []
}
```

![Model predictions](/assets/predictors/mariadb-query.gif)
