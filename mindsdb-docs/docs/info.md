# Machine Learning in Database using SQL

MindsDB is an open-source predictive layer for existing databases that enables rapid prototyping & deployment of ML Models from your database. Significantly reducing the time and cost of machine learning workflows.

![Machine Learning in Database using SQL](https://camo.githubusercontent.com/0a37568c84d116410e4ecb142056b0d8b66b3646105bdcb768bd3ca8c2f6da11/68747470733a2f2f6d696e647364622d7265736f75726365732e73332e616d617a6f6e6177732e636f6d2f4d696e647344422b476c75652e706e67)


# From Database Tables to Machine Learning Model

!!! info "As a quick example, think of a database that stores home rentals sqft and price:"

    ```sql
    SELECT sqft, price FROM home_rentals_table;
    ```

    ![SQFT vs Price](/assets/info/sqft-price.png)

!!! note "You could query the database for information in this table, and if your search criteria have a match, you get results:"
    

    ```sql
    SELECT sqft, price FROM home_rentals_table WHERE sqft = 900;
    ```

    ![SELECT FROM Table](/assets/info/select.png)

!!! note "If there is no match for your search criteria you get empty results:"

    ```sql
    SELECT sqft, price FROM home_rentals_table WHERE sqft = 800;
    ```

    ![SELECT FROM Table No Results](/assets/info/selectm.png)

!!! tip "An ML model could be fitted to the data in the home rentals table."

    ```sql
    CREATE PREDICTOR  home_rentals_model TRAIN FROM home_rentals_table PREDICT price;   
    ```

    ![Model](/assets/info/model.png)

!!! success "An ML model could provide approximate answers for searches where there is no exact match in the income table:"
    

    ```sql
    SELECT sqft, price FROM home_rentals_model WHERE sqft = 800;
    ```

    ![Query model](/assets/info/query.png)
