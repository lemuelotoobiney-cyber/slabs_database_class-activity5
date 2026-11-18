AUTHOR: Lemuel Waye Otoo-Biney
-------------------------------

1.) ER Components
-----------------------------------------------------------------------------
Entity = is a person, place or thing that can be identified,
Relationship = the connection between entities,
Attribute = properties describing an entity. For example a Library/online book
store is an entity and the attributes of the bookstore are the customer name, authors,
book id and more, the relationship between the entity and attributes is that one 
bookstore can own many books online or have many authors books.

2.)Data Model Levels
-------------------------------------------------------------------------------
The Conceptual model describes each entity completely with the it's attributes
and identifies the relationships, this defines what the system contains while the
Physical model describes on what devices the data is stored, how the system will
implemented using a specific DBMS.

Practical ER-to-Relational Conversion
----------------------------------------------------------------------------------
1.) ER Mapping

Conceptual Rule: A customer can place many orders.

Entity 1: Customers(Attributes: customer_id, customer_name )
Entity 2: Orders(Attributes: order_id, item, customer_id )

2. PostgreSQL Implementation
----------------------------------------------------------------------------------
postgres=# CREATE DATABASE store_modeling_db;
CREATE DATABASE
postgres=# \c store_modeling_db
You are now connected to database "store_modeling_db" as user "postgres".
store_modeling_db=# CREATE TABLE customers(
store_modeling_db(# customer_id SERIAL PRIMARY KEY,
store_modeling_db(# customer_name VARCHAR(100) NOT NULL
store_modeling_db(# );
CREATE TABLE
store_modeling_db=# CREATE TABLE orders(
store_modeling_db(# order_id SERIAL PRIMARY KEY,
store_modeling_db(# item VARCHAR(150) NOT NULL,
store_modeling_db(# customer_id INTEGER REFERENCES customers(customer_id)
store_modeling_db(# );
CREATE TABLE
store_modeling_db=# \dt
            List of tables
 Schema |   Name    | Type  |  Owner
--------+-----------+-------+----------
 public | customers | table | postgres
 public | orders    | table | postgres
(2 rows)


store_modeling_db=# INSERT INTO customers(customer_name) VALUES ('Lemmy Otoo'), ('Bruce Wayne');
INSERT 0 2
store_modeling_db=# INSERT INTO orders(items, customer_id) VALUES ('Tomatoes', 1), ('Mirror', 2);
ERROR:  column "items" of relation "orders" does not exist
LINE 1: INSERT INTO orders(items, customer_id) VALUES ('Tomatoes', 1...
                           ^
store_modeling_db=# INSERT INTO orders(item, customer_id) VALUES ('Tomatoes', 1), ('Mirror', 2);
INSERT 0 2
store_modeling_db=# SELECT * FROM customers;
 customer_id | customer_name
-------------+---------------
           1 | Lemmy Otoo
           2 | Bruce Wayne

