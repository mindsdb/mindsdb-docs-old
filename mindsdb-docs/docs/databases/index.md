# Machine Learning Models as Table

Starting from MindsDB 2.0 version you can train machine learning models straight from the database by using MindsDB and the most popular database management systems like MySQL, MariaDB, PostgreSQL, ClickHouse. Any database user can now create, train and test machine learning models with the same knowledge they have of SQL. 

![MindsDB-Databases](/assets/databases/ex-dbs.png)

This integration works by accessing MindsDB as if it is external MySQL database, in short words by exposing machine learning models as tables that can be queried. You simply train the models with an INSERT statement. Then SELECT what you want to predict and you pass in the WHERE statement for the prediction.

![MindsDB-AutoML in Databases](/assets/databases/db-automl.png)

Currently, we are supporting the integration with:

* [MariaDB](/databases/MariaDB)
* [ClickHouse](/databases/Clickhouse)