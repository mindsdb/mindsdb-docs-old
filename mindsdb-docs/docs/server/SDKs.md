
The MindsDB SDK's are providing all of the MindsDB's native functionalities through MindsDB HTTP Interface. Currently, MindsDB provides SDK's for JavaScript and Python.

## Installing JavaScript SDK

The JavaScript SDK can be installed with npm or yarn:

```
npm install mindsdb-js-sdk
```
or

```
yarn add mindsdb-js-sdk
```

Also, you can install it from source:

```
git clone git@github.com:mindsdb/mindsdb_js_sdk.git
cd mindsdb_js_sdk
npm install
```

## Usage example

The following example covers the basic flow: connect to MindsDB Server, train new model, make predictions.

```javascript
import MindsDB from 'mindsdb-js-sdk';

//connection
MindsDB.connect(url);
const connected = await MindsDB.ping();
if (!connected) return;

// lists of predictors and datasources
const predictorsList = MindsDB.dataSources();
const predictors = MindsDB.predictors();

// get datasource
const rentalsDatasource = await MindsDB.DataSource({name: 'home_rentals'}).load();

// get predictor
const rentalsPredictor = await MindsDB.Predictor({name: 'home_rentals'}).load();

// query
const result = rentalsPredictor.queryPredict({'initial)|_price': 2000, 'sqft': 500});
console.log(result);

MindsDB.disconnect();
```

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