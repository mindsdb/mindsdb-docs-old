# Data

In the Data dashboard, you can upload your dataset to MindsDB Server (on your remote/local machine). The available options to upload the data are:

* From the database(MySQL, PostgreSQL, MariaDB, MongoDB, ClickHouse, MsSQL)
* From the local file system 
* From URL

After upload, you will be able to preview (search, sort, order) the data and get the data quality statistics.

![Datasources](/assets/scout/data.png)


## Data Quality

The Data Quality view shows the quality score of each column(input) value and the variability in the dataset. MindsDB looks in every column, analyzes the data, calculates the quality score and shows suggestions and warnings about the data. 

![Datasources Quality](/assets/scout/data-quality.png)
