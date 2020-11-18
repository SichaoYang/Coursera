# Database and SQL for Data Science
Offered by IBM  
https://www.coursera.org/learn/sql-data-science/

## Introduction to Databases
**Data**: A collection of facts in the form of words, numbers, pictures, etc. Data need quick access and security -> database.  
**Database**: A repository of data providing the functionality for adding, modifying, and querying data.  
**Relational Database**: Database that store data in tabular form with columns (item properties) and rows (items), 
allowing data independence logically and physically.  
**DBMS (Database Management System)**: A set of software tools to manage databases,
termed Database, Database Server, Database System, Data Server, and DBMS interchangeably.  
**RDBMS (Relational Database Management System)**: A set of software tools to manage relational databases, 
e.g., MySQL, Oracle Database, IBM Db2, etc.  
**SQL (Structured Query Language)**: A language used for relational databases to query data.

### Relational Database Concepts
**ER (Entity-Relationship) Model**: A data model composed of enetity types and entity relationships, illustrated as an ER diagram.
- **Entity**: 
  - Object that exists independently of any other entities in the database.
  - E.g., book. 
  - Drawn as rectangles in an ER diagram. 
  - Maps to a table in a relational database.
- **Attributes**: 
  - Properties or characteristics of an entity.
  - E.g., title, edition, year, etc. of a book.
  - Drawn as ovals in an ER diagram. 
  - Maps to columns in a table.
  - Datatypes: characters, numbers, datas/times, etc.
  - A **Primary Key** uniquely identifies a specific row in a table.
  
### Basic SQL
**SQL Statement** types:
- **DDL (Data Definition Language)**: Define tables.
  - CREATE: create tables and define its columns.
  ```sql
  CREATE TABLE <table_name>
    (
     <column_name_1> <datatype> [optional_parameters],
     ...
     <column_name_n> <datatype>
    )
  /* e.g. */
  CREATE TABLE provinces
    (
     id char(2) PRIMARY KEY NOT NULL,
     name varchar(24)
    )
  ```
  - ALTER: alter tables: add/drop columns and modify column data types.
  - TRUNCATE: delete data in a table.
  - DROP: delete tables.

**DML (Data Manipulation Language)**: Read and modify data in a table with 
CRUD (Create, Read, Update, and Delete rows) operations.
  - INSERT: insert a row or rows of data into a table.
  ```sql
  INSERT INTO <table_name> 
      (<column_name_1>, ..., <column_name_n>)
  VALUES (<value_1>, ..., <value_n>)
  /* e.g. */
  INSERT INTO AUTHOR
      (AUTHOR_ID, LASTNAME, FIRSTNAME, CITY, COUNTRY)
  VALUES 
      ('A1', 'Chong', 'Raul', 'Toronto', 'CA')
      ('A2', 'Ahuja', 'Rav',  'Toronto', 'CA')
  
  ```
  - SELECT: retrieve a row or rows of data from a table.
  ```sql
  /* Select statement: Query
     Select result:    Result set/table */
     
  select * from <table_name>
  select <column_name_1>, ..., <column_name_n> from <table_name>
  select ... from <table_name> WHERE <predicate>
  /* e.g. */
  select book_id, title from Book where book_id = 'B1'  /* = > < >= <= <> */
  
  select COUNT(...) from <table_name>
  /* e.g. */
  select count(COUNTRY) from MEDALS where COUNTRY = 'CANADA'
  
  select DISTINCT <column_name> from <table_name>
  /* e.g. */
  select distinct COUNTRY from MEDALS where MEDALTYPE = 'GOLD'
  
  select ... from <table_name> LIMIT <number_of_rows>
  /* e.g. */
  select * from MEDALS where YEAR = 2018 limit 5
  ```
  - UPDATE: edit a row or rows of data in a table.
  ```sql
  UPDATE <table_name>
  SET <column_name_1> = <value_1> ... <column_name_n> = <value_n>
  [WHERE <condition>]
  /* e.g. */
  UPDATE AUTHOR
  SET LASTNAME = 'KATTA' 
      FIRSTNAME = 'LAKSHMI'
  WHERE AUTHOR_ID = 'A2'
  ```
  - DELETE: remote a row or rows of data from a table.
  ```sql
  DELETE FROM <table_name> [WHERE <condition>]
  /* e.g. */
  DELETE FROM AUTHOR WHERE AUTHOR_ID IN ('A2', 'A3')
  ```
