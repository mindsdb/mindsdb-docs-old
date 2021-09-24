# What is MindsDB?

MindsDB enables advanced predictive capabilities directly in the Database. This puts sophisticated machine learning techniques into the hands of those who know SQL, such as, data analysts, developers and business intelligence users without the need for a new tool or significant training. 

Data is the single most important ingredient in machine learning, and your data lives in a database. So why do machine learning anywhere else? 


![Machine Learning in Database using SQL](/assets/mdb_image.png)

## The Vision:

***A world where people use intelligent databases to make better data-driven decisions.***

We think the best strategy to do this is to enable ML capabilities for existing databases rather than to create another one. (You can think of MindsDB as Intelligence for exsiting Databases). 


## From Database Tables to Machine Learning Models

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


## Getting started

To start using MindsDB, check out our [Getting started guide](/info)
