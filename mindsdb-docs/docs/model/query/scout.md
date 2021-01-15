# Query the model using Scout

To get predictive analytics from trained model:

1. From the left navigation menu open `Query` dashboard.
2. Click on the `NEW QUERY` button.
3. In the `New Query` modal:
    1. Select the `From` predictor option(the name of the pre trained model).
    2. Add the features values for which you want to get the predictions.

## Query the UsedCars model example

In this example we want to solve the problem of estimating the right price for a used car that has Diesel as a fuel type and has around 20 000 miles. To get the price:

1. From the predictors dashboard click on the `Query` button.
2. Click on the `NEW QUERY` button.
3. In the `New Query` modal:
    1. Add the features values for which you want to get the predictions e.g
        1. Mileage 20 000.
        2. Fuel type Diesel.

![Query from Scout](/assets/predictors/query-scout.gif)