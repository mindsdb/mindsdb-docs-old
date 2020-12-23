# Query the model from ClickHouse database

This section assumes that you have trained new model using [clickhouse-client](/model/clickhouse/) or [MindsDB Scout](model/train/). To query the model, you will neeed to `SELECT` from the model table as:

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
    Note that even if you have trained the model from the ClickHouse database, you will be able to query it from other databases too.

## Query example

The following example shows you how to train new model from clickhouse-client. The table used for training the model is timeseries data same as [Air Pollution in Seoul](https://www.kaggle.com/bappekim/air-pollution-in-seoul) dataset. MindsDB will predict the `SO2` (Sulfur dioxide) value in the air based on the values added in `WHERE` statement.

```sql
SELECT 
    SO2 AS predicted,
    SO2_confidence AS confidence,
    SO2_explain AS info
FROM airq_predictor
WHERE (NO2 = 0.005) AND (CO = 1.2) AND (PM10 = 5)
```
You should get a similar response from MindsDB as:

| SO2  | confidence | info   |
|----------------|------------|------|
| 0.009897379182791115 | 0.99 | Check JSON bellow  |

```json
info:{
    "predicted_value": 0.009897379182791113, 
    "confidence": 0.99, 
    "prediction_quality": "very confident", 
    "confidence_interval": [0.0059810733322441575, 0.01381368503333807], "important_missing_information": ["Address"]
}
```

![Model predictions](/assets/predictors/clickhouse-query.gif)
