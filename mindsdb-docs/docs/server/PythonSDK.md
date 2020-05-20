# MindsDB's Python SDK

The MindsDB SDK for Python provides all of the MindsDB's native functionalities through MindsDB Server.

## Installing Python SDK

The Python SDK can be installed from PyPI:

```
pip install mindsdb-client
```

Or you can install it from source:

```
git clone git@github.com:mindsdb/mindsdb_python_sdk.git
cd mindsdb_python_sdk
python setup.py develop
pip install -r requirements.txt
```

## Usage example

The following example covers the basic flow: connect to MindsDB Server, train new model, make predictions.

```python
from mindsdb_client import MindsDB

# connect
mdb = MindsDB(server='http://mindsdb.server:47334', params={'email': 'login@email.com', 'password': 'loginpass'})

# upload datasource
mdb.datasources.add('home_rentals_data', path='home_rentals.csv')

# create a new predictor and learn to predict
predictor = mdb.predictors.learn(
    name='home_rentals',
    data_source_name='home_rentals_data',
    to_predict='rental_price'
)

# predict
result = predictor.predict({'initial_price': '2000','number_of_bathrooms': '1', 'sqft': '700'})
```