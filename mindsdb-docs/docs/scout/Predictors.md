# Predictors

The Predictor, in MindsDB’s words, means the machine learning model. In this dashboard, you will train the models from the Datasources. The available options are to Upload the already existing model or Train a New one.

![Predictors](/assets/scout/predictors.png)


## Basic Mode

To Train New Predictor, the required options are the Predictor Name and the columns to be predicted (target variables).

![Predictor Basic](/assets/scout/predictor-basic.png)


## Advanced Mode

Inside the Advanced Mode, you can specify additional options before training new Predictor as:

* `Sample Margin of Error`: the amount of random sampling error.
* `Stop Training After`: stop the model training after `n ` minutes.
* `Backend`: the Machine Learning backend to use for training ([Lightwood](https://github.com/mindsdb/lightwood) or [Ludwig](https://github.com/uber/ludwig)).
* `Use GPU`: use Graphics Processing Unit for training.
* `Select columns to be removed for training`: speed the training or improve accuracy by ignoring un relevant columns.

![Predictor Advanced](/assets/scout/predictor-advanced.png)

## Predictor Results

The Predictor Results dashboard, provides powerful insights related to the model. The 3 important questions that this section answers are:

* How accurate is the model?
* What is relevant for this model?
* When can you trust this model?

![Predictor Quality](/assets/scout/predictor-quality.png)
