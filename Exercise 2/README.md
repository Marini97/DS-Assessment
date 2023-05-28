# Exercise 2 - Product Sales
This exercise is about SQL and data management. You have to answer questions by commenting on your answers.

Suppose that you work for a company whose main business is selling products on an e-commerce website.

You have the following tables organized in a database:
- customers
    - id
    - firstname
    - lastname
    - data_of_birth
    - country
- orders
    - id
    - id_customer
    - order_cost
- orders_items
    - id
    - id_order
    - id_product
    - quantity
- products
    - id
    - name
    - price

## Questions:
1. Can you explain the purpose of the `orders_items` table?
2. Can you write a SQL query to find the average order cost per country?
3. Can you write a SQL query to find the name of the highest price product sold to an Italian customer?
4. How could you optimize the orders table assuming you have to manage a lot of queries?
5. What would you change if the amount of data is too big to run these queries? (suppose to have 500TB of data)

## Responses:
1. 
   The `orders_items` table is a join table that allows for a many-to-many relationship between orders and products. It allows for a single order to contain multiple products, and for a single product to be contained in multiple orders.
2. 
    ```sql
    SELECT c.country, AVG(o.order_cost) AS avg_order_cost
    FROM customers c
    JOIN orders o ON c.id = o.id_customer
    GROUP BY c.country
    ```
    First it joins the `customers` and `orders` tables. Then it groups the results by country, and finally it calculates the average order cost by using the aggregate function `AVG`.

3. 
    ```sql
    SELECT p.name
    FROM products p
    JOIN orders_items oi ON p.id = oi.id_product
    JOIN orders o ON oi.id_order = o.id
    JOIN customers c ON o.id_customer = c.id
    WHERE c.country = 'Italy'
    ORDER BY p.price DESC
    LIMIT 1
    ```
    To do this task we've to join all the tables, then filter the results by country = 'Italy'. Finally, we order the results by price in **descending** order, and we take the first result as the highest price product sold to an Italian customer.


4. 
   Since the `orders` Table is accessed a lot, I would add an index on the `id_customer` column. This would speed up the queries that join the `orders` table with the `customers` table. https://www.w3schools.com/sql/sql_create_index.asp


5. 
    There are a few things that can be done to improve the performance:
    - **Partitioning**: it's a technique that splits large tables into smaller ones. This can improve the performance of the queries if the rows most used are in a single partition or small number of partitions. https://www.postgresql.org/docs/current/ddl-partitioning.html
    - **Sharding**: It's similar to **partitioning**, but it splits the data across multiple servers. https://ieeexplore.ieee.org/document/9835604

