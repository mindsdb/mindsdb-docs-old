---
id: comparison-mindsdb
title: Comparison with other Libraries
---

Let's compared Mindsdb with some popular deep learning and machine learning libraries to show what makes it different.

## Models

With libraries such as Tensorflow, Sklearn, Pytorch you must have the expertise to build models from scratch. Your models are also black boxes, you can't be sure how or why they work and you have to pre-process your data in a format that's suitable for the model and look for any errors in the data yourself.

With Mindsdb anyone can build state of the art models without any machine learning knowledge. Mindsdb also provides data extraction, analyses your input data and analyses the resulting model to try and understand what makes it work and what types of situations it works best in.

## Data Preprocessing

Building models require time for cleaning the data, normalizing the data, converting it into the format your library uses, determining the type of data in each column and a proper encoding for it

Mindsdb can read data from csv, json, excel, file urls, s3 objects , dataframes and relational database tables or queries (currently there's native support for maraiadb, mysql and postgres), you just need to tell it which colum(s) it should predict. It will automatically process the data for you and give insights about the data.


## Code Samples

We are going to use **[home_rentals.csv](https://s3.eu-west-2.amazonaws.com/mindsdb-example-data/home_rentals.csv)** dataset for comparison purpose.

Our goal is to predict the rental_price of the house given the information we have in `home_rental.csv`.

We will look at doing this with Sklearn, Tensorflow, Ludwig and Mindsdb.

* Sklearn is a generic easy-to-use machine learning library.
* Tensorflow is the state of the art deep learning model building library from google.
* Ludwig is a library from Uber that aims to help people build machine learning models without knowledge of machine learning (similar to mindsdb)

### Preprocessing

*Note: This step is only required for Sklearn and Tensorflow, for Ludwig and mindsdb we will be using the raw csv file*

When working with data we first have to see what type of data we are dealing with, in our case we have some numerical, categorical data. We first need to convert categorical data columns into numerical data.

```python
# loading data
import pandas as pd
data = pd.read_csv("home_rentals.csv")

# dealing with categorical values
data=pd.get_dummies(data, prefix=['condition','type'], columns=['location','neighborhood'])

# splitting data into train and test set
from sklearn.model_selection import train_test_split
train_data, test_data = train_test_split(data, test_size=0.2)

# seperating the input and output
train_label = train_data['rental_price']
test_label = test_data['rental_price']
del train_data['rental_price']
del test_data['rental_price']
```

### Building the model

Now we will build the actual models to train on the training dataset and run some predictions on the testing dataset. For the purpose of this example, we'll build a simple linear regression with both Tensorflow and Sklearn, in order to keep the code to a minimum.

#### Tensorflow

```python
# placeholders for input data and label
X = tf.placeholder('float')
Y = tf.placeholder('float')

W = tf.Variable(tf.random.normal(), name = "weight")
b = tf.Variable(tf.random.normal(), name = "bias")

learning_rate = #your learning rate
epochs = # no of times data should be fed

y_pred = tf.add(tf.multiply(X, W), b)
cost = tf.reduce_sum(tf.pow(y_pred-Y, 2)) / (2 * len(train_data))
# Choosing the optimizer
optimizer = tf.train.GradientDescentOptimizer(learning_rate).minimize(cost)
# Initialize the Global variables
init = tf.global_variables_initializer()

# Run inside a session
with tf.Session() as sess:
    sess.run(init)
    for epoch in range(epochs):
        # feeding the training data
        for (_x, _y) in zip(train_data, train_label):
            sess.run(optimizer, feed_dict = {X : _x, Y : _y})
        # Calculate the cost
        c = sess.run(cost, feed_dict = {X : train_data, Y : train_label})
        print("epoch", (epoch + 1), ": cost =", c, "W =", sess.run(W), "b =", sess.run(b))
    # save your weights and bias
    weight = sess.run(W)
    bias = sess.run(b)

# Getting the predictions
predictions = weight* (test_data) + bias
print(predictions)
```

#### Sklearn

```python
from sklearn import datasets, linear_model
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
import pandas as pd

#load data
data = pd.read_csv("train.csv")
#target value
labels = data['rental_price']
train1 = data.drop(['rental_price'],axis=1)

#train test split
x_train , x_test , y_train , y_test = train_test_split(train1 , labels)

# label encode values
le = LabelEncoder()
le.fit(x_train['location'].astype(str))
x_train['location'] = le.transform(x_train['location'].astype(str))
x_test['location'] = le.transform(x_test['location'].astype(str))

le.fit(x_train['neighborhood'].astype(str))
x_train['neighborhood'] = le.transform(x_train['neighborhood'].astype(str))
x_test['neighborhood'] = le.transform(x_test['neighborhood'].astype(str))

# Create linear regression object
regr = linear_model.LinearRegression()

# Train the model using the training sets
regr.fit(x_train, y_train)

# Make predictions using the testing set
prediction = regr.predict(x_test)

# The coefficients
print('Prediction ', prediction)
print('Coefficients: \n', regr.coef_)

# The mean squared error
print('Mean squared error: %.2f'
      % mean_squared_error(y_test, prediction))
# The coefficient of determination: 1 is perfect prediction
print('Coefficient of determination: %.2f'
      % r2_score(y_test, prediction))
```

#### Ludwig

```python
from ludwig.api import LudwigModel

import pandas as pd

# read data
train_dataf = pd.read_csv("train.csv") 
# defining the data
model_definition = {
    'input_features':[
        {'name':'number_of_rooms', 'type':'numerical'},
        {'name':'number_of_bathrooms', 'type':'numerical'},
        {'name':'sqft', 'type':'numerical'},
        {'name':'location', 'type':'text'},
        {'name':'days_on_market', 'type':'numerical'},
        {'name':'initial_price', 'type':'numerical'},
        {'name':'neighborhood', 'type':'text'},
    ],
    'output_features': [
        {'name': 'rental_price', 'type': 'numerical'}
    ]
}
# creating and training the model
model = LudwigModel(model_definition)
train_stats = model.train(data_df=train_dataf)

# read test data
test_dataf = pd.read_csv("test.csv")

#predict data
predictions = model.predict(data_df=test_dataf)

print(predictions)
model.close()
```

*Note: If the data is inconsistent or of erroneous, null value it may throw an error. So you may want to  preprocess/clean  the data first.*

### Mindsdb

```python
from mindsdb import Predictor

# tell mindsDB what we want to learn and from what data
Predictor(name='home_rentals_price').learn(
    to_predict='rental_price', # the column we want to learn to predict given all the data in the file
    from_data='train.csv' # the path to the file where we can learn from, (note: can be url)
)
# use the model to make predictions
result = Predictor(name='home_rentals_price').predict(when={'number_of_rooms': 2, 'initial_price': 2000, 'number_of_bathrooms':1, 'sqft': 1190})

# now print the results
print('The predicted price is between ${price} with {conf} confidence'.format(price=result[0].explanation['rental_price']['confidence_interval'], conf=result[0].explanation['rental_price']['confidence']))
```

Generally speaking, Mindsdb differentiates itself from other libraries by its **simplicity**. Lastly, [Mindsdb Scout](https://www.mindsdb.com/product) provides you with an easy way to visiualize more insights about the model. This can also be done by calling `mdb.get_model_data('model_name')`, but it's easier to use Mindsdb Scout to visualize the data, rather than looking at the raw json.
