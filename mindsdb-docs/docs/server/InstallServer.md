# MindsDB Server

The [MindsDB Server](https://github.com/mindsdb/mindsdb_server) is an HTTP interface that makes MindsDB easy to use from different programming languages.

## Installing MindsDB Server

The MindsDB Server can be installed from PyPi:

```python
pip install mindsdb-server
```

Or you can install it from source:

```python
git clone git@github.com:mindsdb/mindsdb_server.git
cd mindsdb_server
python setup.py develop
pip install -r requirements.txt
```

## Start the Server

To start MindsDB Server simply call the `start_server()` function:

```python
import mindsdb_server as server
server.start_server()
```

The default port for the server is 47334, but you can provide port parameter to change it:
```python
server.start_server(port=47335)
```

## MindsDB Server API's

The detailed information for each endpoint can be found on the [api.docs.mindsdb](https://apidocs.mindsdb.com/?version=latest). 
You can choose the example API request for your prefered programming language by simply changing the LANGUGE dropdown.