# MindsDB's JavaScript SDK

The MindsDB SDK for JavaScript provides all of the MindsDB's native functionalities through MindsDB Server.

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