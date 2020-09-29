# Introduction to MindsDB Scout

MindsDB Scout is a graphical user interface that sits on top of MindsDB and MindsDB Server. It lets you to upload, analyze and visualize your data, train machine learning models and query them with few clicks directly from the Databases, your local file system or external resources.


## Download MindsDB Scout(Depricated option)

MindsDB Scout works on the most widely used operating systems. One of the requirements before installing it is to have Python >=3.6 installed. You can download it for free from the [MindsDB product page](https://www.mindsdb.com/product).

## Start Scout

```
 python3 -m mindsdb --api=http,mysql
```

When MindsDB server is started it will display the URL for accessing Scout:

```
GUI should be available by http://0.0.0.0:47334/static/index.html
```

Open up `http://0.0.0.0:47334/static/index.html` on your browser and the Scout should be started

## Tutorial
We have created a few tutorials that will help you to successfully install and use MindsDB Scout:

* [An Overview of MindsDB Scout](https://www.mindsdb.com/blog/mindsdb-scout-overview)
* [Perform Data Science with MindsDB Scout](https://www.mindsdb.com/blog/data-science-with-scout)
 <iframe width="560" height="315" src="https://www.youtube.com/embed/fOwdv4j26CA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Overview of MindsDB Scout

The MindsDB Scout interface is divided into 5 dashboards.

* [Connection](/scout/Connection)
* [Databases](/scout/Databases)
* [Datasets](/scout/Datasources)
* [Predictors](/scout/Predictors)
* [Query](/scout/Query)
