# Evaluate model quality using Scout

Once the model is trained you can use the model quality preview to get insights about the trained model.

!!! question "Visualize model quality"
    Note that any model could be evaluated using MindsDB Scout. That means not only the models
    trained with Scout but also models trained from SQL clients, MindsDB API's or SDK.

To do that:

1. From the left navigation menu select the `Predictors` dashboard.
2. Click on the `PREVIEW` button on the model you want to evaluate. 
3. Click on the minus sign to expand each section.

![Model quality info](/assets/predictors/model-quality.gif)

### Model Accuracy

In this section MindsDB will show you the visualizations about:

* Data splitting (80% train data and 20% test data)
* Model accuracy (How accurate is the model when blindsided) 

![Model accuracy](/assets/predictors/model-accuracy.png)

### Column importance

This section tries to answer the `What is important for this model?` question. MindsDB tries various combinations of missing columns to determine the importance of each one. The column importance rating ranges from 0 which means the column is useless to 10 meaning the column's predictive ability is great.

![Column importance](/assets/predictors/column-importance.png)

### Confusion matrix

This section tries to answer the `When can you trust this model?` question. 
Here, the confusion matrix shows the performance that the model gets when solving a classification problem. Each entry in the confusion matrix can tell how many samples of each class were correctly classified and how many and where incorrectly classified. To get a detailed explanation you can move the mouse cursor over the graphics.

![Confusion matrix](/assets/predictors/confusion-matrix.png)


!!! Success "Let's Query the model :bar_chart: :mag_right:"
    After evaluating the performance of the model, next step is to get predictions by [querying the model](/model/query/scout/).