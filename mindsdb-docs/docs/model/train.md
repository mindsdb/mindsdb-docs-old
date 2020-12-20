# Train new model using Scout

Before training the new model you must connect to a Datasource. To learn how to do that check out:

* [Connect to MySQL documentation](/datasources/mysql).
* [Connect to PostgreSQL documentation](/datasources/mysql).

### Basic mode

Training the new model from MindsDB Scout is quite easy:

1. From the left navigation menu open `Predictors` dashboard.
2. Click on the `TRAIN NEW` button.
3. In the `New Predictor` modal:
    1. Select the `From` datasource option.
    2. Add the name of the model.
    3. Check the column name (feature) that you want to predict.
    4. Press `TRAIN`. 

![Train model basic mode](/assets/predictors/train-basic.gif)

### Advanced mode

In the `Advanced mode`, you can find a few additional options to train the Machine Learning model as use GPU for training, exclude columns from training or change the sample margin of error. To do that, inside the `New Predictor` modal:

1. Select the `From` datasource option.
2. Add the name of the model.
3. Check the column name (feature) that you want to predict.
4. Press the `ADVANCED MODE` button and:
    1. Check the `USE GPU` checkbox.
    2. Check the columns that you want to exclude from model training.
    3. Add the `sample margin of error` value.
5. Press `TRAIN`. 

![Train model advanced mode](/assets/predictors/train-advanced.gif)


!!! Success "That's all :tada: :trophy:  :computer:"
    You have successfully trained a new Machine Learning model. The next step is to evaluate the [model quality](/model/quality).