---
id: timeseries-mindsdb
title: Handling Timeseries Data
---

## Handling Timeseries Data

### Timeseries interface

A timeseries is a problem where rows are related to each other in a sequential way, such that the prediction of the value in the present row should take into account a number of previous rows.

To build a timeseries model you need to pass `timeseries_settings` dictionary to `learn`

```
timeseries_settings = {
  order_by: List<String>              | Mandatory
  group_by: List<String>              | Optional (default: [])
  nr_predictions: Int                 | Optional (default: 1)
  use_previous_target: Bool           | Optional (default: True)
  keep_order_column:   Bool           | Optional (default: True)
  window: Int                         | Mandatory if `dynamic_window` is not passed
  dynamic_window: Int                 | Mandatory if `window` is not passed
  historical_columns: List<String>    | Optional (default: [])
}
```

Let's go through these settings one by one:

* order_by - The columns based on which the data should be ordered
* group_by - The columns based on which to group multiple unrelated entities present in your timeseries data. For example, let's say your data consists of sequential readings from 3x sensors. Treating the problem as a timeseries makes sense for individual sensors, so you would specify: `group_by=['sensor_id']`
* nr_predictions - The number of points in the future that predictions should be made for, defaults to `1`. Once trained, the model will be able to predict up to this many points into the future.
* use_previous_target - Use the previous values of the target column[s] for making predictions. Defaults to `True`. [Status: Experimental]
* keep_order_column - Whether or not to use the column[s] based on which the data is ordered for making predictions. This might be relevant if the order columns is, for example, a simple auto-incrementing index. Defaults to `True`. [Status: Not Implemented]
* window - The number of rows to "look back" into when making a prediction, after the rows are ordered by the order_by column and split into groups.
* dynamic_window - The number of seconds to "look back" into when making a prediction, this argument is mutually exclusive with `window`. The `window` argument could be used to specify something like "Always use the previous 10 rows", while this argument is used to specify something like "Always use the previous 10 hours" (which can result in a variable number of rows for each sample).

### Code example

```python
import mindsdb

mdb = mindsdb.Predictor(name='assembly_machines_model')
mdb.learn(
    from_data='assembly_machines_historical_data.tsv',
    to_predict='failure'
    ,timeseries_settings = {
      order_by: ['timestamp'] # Order the observations by timestamp
      group_by: ['machine_id'] # The ordering should be done on a per-machine basis, rather than for every single row
      nr_predictions: 3 # Predict failures for the timestamp given and for 2 more timesteps in the future
      use_previous_target: True # Us the previous values in the target column (`failure`), since when the last failure happened could be a relevant data-point for our prediction.
      keep_order_column: False #The timestamp of the sample should have no relevance to the machine failing, it's just here to order the observations, so we won't be using it for making predictions, just for ordering.
      window: 20 # Consider the previous 20 rows for every single row our model is trying to predict o
    }
)

results = mdb.predict(when_data='assembly_machines_data.tsv')
```

### Historical data
When making timeseries predictions, it's important to provide mindsdb with the context for those predictions, i.e. with the previous rows that came before the one you are trying to predict for.

This can be done automatically when using mindsdb from within a database (see bellow) or manually by passing the historical data as part of the structured file or dataframe given to `when_data`.

Historical data should contain one additional columns called `make_predictions` which can be set to `true` or `false`, this column should be set to `false` for all rows that are there to simply provide historical context. Also, make sure to provide the values for the target columns for all rows that are there to provide historical context if `use_previous_target` is set to `True`.


### Database integration
When querying the original training data (the one passed to `learn`) from a database, mindsdb is able to automatically infer the queries required to get historical data for the `predict` calls in order to provide the previous rows for a given sample that we want to predict for.


### Database example (from SQL)
-- Pending, feel free to contribute some or ask us directly about this feature

### Database example (from code)
-- Pending, feel free to contribute some or ask us directly about this feature
