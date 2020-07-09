---
id: predictor-interface
title: Predictor interface
---

This section goes into detail about each of the methods exposed by mindsdb_native and each of the arguments they work with.

## Predictor

### Constructor

`predictor = Predictor(name='blah')`

Constructs a new mindsdb predictor

* name -- Required argument, the name of the predictor, used for saving the predictor, creating a new predictor with the same name as a previous one loads the data from the old predictor
* root_folder -- The directory (also known as folder) where the predictor information should be saved
* log_level -- The log level that the predictor should use, number from 0 to 50, with 0 meaning log everything and 50 meaning log only fatal errors:
```python
DEBUG_LOG_LEVEL = 10
INFO_LOG_LEVEL = 20
WARNING_LOG_LEVEL = 30
ERROR_LOG_LEVEL = 40
NO_LOGS_LOG_LEVEL = 50
```

### Get Models

`predictor.get_models()`

Takes no argument, returns a list with all the models and some information about them

**Note: this is akin to a static method, it acts the same way no matter what predictor object you call it on, but due to various consideration it hasn't been swtiched to a static method yet**

### Get Model Data

`predictor.get_model_data(model_name='model_name')`

Returns all the data we have about a given model, this is a rather complex python dictionary meant to be interpreted by the Scout GUI, we recommend looking at the training logs mindsdb_native gives to see some of these insight in an easy to read format.

* model_name -- Required argument, the name of the model to return data about.

**Note: this is akin to a static method, it acts the same way no matter what predictor object you call it on, but due to various consideration it hasn't been swtiched to a static method yet**

### Export Model

`predictor.export_model()`

Exports this predictor's data (or the data of another predictor) to a zip file inside the directory you call it from.

* model_name -- The name of the model to export (defaults to the name of the current Predictor).

### Load

`predictor.load(mindsdb_storage_dir='path/to/predictor.zip')`

Loads a predictor that was previously exported into the current mindsdb_native storage path so you can use it later.

* mindsdb_storage_dir -- full_path that contains your mindsdb_native predictor zip file.

### Load Model

Backwards compatible interface for the `load` functionality that can be called as `load_model` instead.

### Delete Model

`predictor.delete_model(model_name='blah')`

Deletes a given predictor from the storage path mindsdb_native is currently operating with.

* model_name -- The name of the model to delete (defaults to the name of the current Predictor).

### Analyse dataset

`predictor.analyse_dataset(from_data=a_data_source)`

Analyse the dataset inside the data source, file, ulr or pandas dataframe given. This runs all the steps prior to actually training a predictive model

* from_data -- the data that you want to analyse, this can be either a file, a pandas data frame, a url or a mindsdb data source.
* sample_margin_of_error -- Maximum expected difference between the true population parameter, such as the mean, and the sample estimate. Essentially, if this argument has a value bigger than 0 Mindsdb will not run the data analysis phase on all the data, but rather select a sample, if your dataset is large (> 10,000 rows) or has a lot of columns or a lot of text or multimedia columns, you might find it speeds up mindsdb_native quite a lot to give this argument a value between `0.05` and `0.15`, avoid going above `0.2` as a general rule of thumb. (default to 0).

### Learn

`predictor.learn(from_data=a_data_source, to_predict='a_column')`

Teach the predictor to make predictions on a given dataset, extract information about the dataset and extract information about the resulting machine learning model making the predictions. This is the "main" functionality of mindsdb_native together with the "predict" method.

* from_data -- the data that you want to use for training, this can be either a file, a pandas data frame, a url or a mindsdb data source.

* to_predict -- The columns/keys to be predicted (aka the targets, output columns, target variables), can be either a string (when specifying a single column) or a list of strings (when specifying multiple columns).

* test_from_data -- Specify a different data source on which mindsdb should test the machine learning model, by default mindsdb_native takes testing and validation samples from your dataset to use during training and analysis, and only trains the predictive model on ~80% of the data. This might seem sub-optimal if you're not used to machine learning, but trust us, it allows us to have much better confidence in the model we give you.

*  **timeseries specific parameters**: group_by, window_size, order_by -- For more information on how to use these, please see the [advanced examples section dealing with timeseries](https://mindsdb.github.io/mindsdb/docs/advanced-mindsdb#timeseries-predictions). Please note, these are currently subject to change, though they will remain backwards compatible until v2.0.

* ignore_columns -- Ignore certain columns from your data entirely.

* stop_training_in_x_seconds -- Stop training the model after this amount of seconds, note, the full amount it takes for mindsdb_native to run might be up to twice the amount you specify in this value. Thought, usually, the model training constitutes ~70-90% of the total mindsdb_native runtime.

* stop_training_in_accuracy -- Deprecated argument, left for backwards compatibility, to be removed or revamped in v2.0, refrain from using, it has no effects.

* backend -- The machine learning backend to use in order to train the model. This can be a string equal to `lightwood` (default) or `ludwig`, this can also be a custom model object, for an example of those this works, please see [this example](https://github.com/mindsdb/mindsdb/blob/master/tests/functional_testing/custom_model.py).

* rebuild_model -- Defaults to `True`, if this is set to `False` the model will be loaded and the model analysis and data analysis will be re-run, but a new model won't be trained.

* use_gpu -- Defaults to `None` (autodetect), set to `True` if you have a GPU and want to make sure it's used or to `False` if you want to train the model on the CPU, this will speed up model training a lot in most situations. Note, that the default learning backend (lightwood) only work with relatively new (2016+) GPUs.

* equal_accuracy_for_all_output_categories -- When you have unbalanced target variable values, this will treat all of them as equally important when training the model. To see more information about this and an example, please see (this section)[https://docs.mindsdb.com/tutorials/AdvancedExamples/#unbalanced-dataset]

* output_categories_importance_dictionary -- A dictionary containing a number representing the importance for each (or some) values from the column to be predicted. An example of how his can be used (assume the column we are predicting is called `is_true` and takes two falues): `{'is_true': {'True':0.6, 'False':1}}`. The bigger the number (maximum value is one), the more important will it be for the model to predict that specific value correctly (usually at the cost of predicting other values correctly and getting more false positives for that value).

* advanced_args -- A dictionary of advanced arguments. Includes `force_disable_cache`, `force_categorical_encoding`, `handle_foreign_keys`,
`use_selfaware_model`, `deduplicate_data`.

* sample_settings -- A dictionary of options for sampling from the dataset. Includes `sample_for_analysis`. `sample_for_training`, `sample_margin_of_error`, `sample_confidence_level`, `sample_percentage`, `sample_function`.

If you are interested in using advanced_args or sample_settings but you are unsure of how they work, please shot us an email or create a github issue and we will help you.

## Predict
`predict(self, when_data = None, update_cached_model = False, use_gpu=False, advanced_args={}, backend=None, run_confidence_variation_analysis=False):`

`predictor.predict(from_data=a_data_source)`

Make a prediction about a given dataset.

* when_data -- the data that you want to make the predictions for, this can be either a file, a pandas data frame, a url, a dictionary used for single prediction(column name: value) or a mindsdb data source.

* update_cached_model -- Deprecated argument, left for backwards compatibility, to be removed or revamped in v2.0, refrain from using, it has no effects.

* use_gpu -- Defaults to `None` (autodetect), set to `True` if you have a GPU and want to make sure it's used or to `False` if you want to train the model on the CPU, this will speed up model training a lot in most situations. Note, that the default learning backend (lightwood) only work with relatively new (2016+) GPUs.

* advanced_args -- A dictionary of advanced arguments. Includes `force_disable_cache`.

* backend -- The machine learning backend to use in order to train the model. This can be a string equal to `lightwood` (default) or `ludwig`, this can also be a custom model object, for an example of those this works, please see [this example](https://github.com/mindsdb/mindsdb/blob/master/tests/functional_testing/custom_model.py). Note, you shouldn't use a different backend than the one you used to train the model, this will result in undefined behavior in the worst case scenario and most likely lead to a weired error. This defaults to whatever backend was last used when calling `learn` on this predictor.

* run_confidence_variation_analysis -- Run a confidence variation analysis on each of the given input column, currently only works when making single predictions via `when_data`. It provides some more in-depth analysis of a given prediction, by specifying how the confidence would increase/decrease based on which of the columns in the prediction were not present (had null, None or empty values).


## DataSources

Mindsdb exposes a number of data sources that can be used with the predictor, you can find the documentation detailing this [here](https://mindsdb.github.io/mindsdb/docs/data-sources)

## Constants and Configuration

For the constants and configuration options exposed by mindsdb_native at large please refer to [this section](/Config/).
