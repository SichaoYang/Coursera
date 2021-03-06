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
    );
  /* e.g. */
  create table provinces
    (
     id char(2) PRIMARY KEY NOT NULL,
     name varchar(24)
    );
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
  VALUES (<value_1>, ..., <value_n>);
  /* e.g. */
  insert into AUTHOR
      (AUTHOR_ID, LASTNAME, FIRSTNAME, CITY, COUNTRY)
  values 
      ('A1', 'Chong', 'Raul', 'Toronto', 'CA'),
      ('A2', 'Ahuja', 'Rav',  'Toronto', 'CA');
  
  ```
  - SELECT: retrieve a row or rows of data from a table.
  ```sql
  /* Select statement: Query
     Select result:    Result set/table */
     
  SELECT * FROM <table_name>
  select <column_name_1>, ..., <column_name_n> from <table_name>
  select ... from <table_name> WHERE <predicate>
  /* e.g. */
  select book_id, title from Book where book_id = 'B1';  /* = > < >= <= <> */
  
  select COUNT(...) from <table_name>;
  /* e.g. */
  select count(COUNTRY) from MEDALS where COUNTRY = 'CANADA';
  
  select DISTINCT <column_name> from <table_name>;
  /* e.g. */
  select distinct COUNTRY from MEDALS where MEDALTYPE = 'GOLD';
  
  select ... from <table_name> LIMIT <number_of_rows>;
  /* e.g. */
  select * from MEDALS where YEAR = 2018 limit 5;
  ```
  - UPDATE: edit a row or rows of data in a table.
  ```sql
  UPDATE <table_name>
  SET <column_name_1> = <value_1> ... <column_name_n> = <value_n>
  [WHERE <condition>];
  /* e.g. */
  UPDATE AUTHOR
  SET LASTNAME = 'KATTA' 
      FIRSTNAME = 'LAKSHMI'
  where AUTHOR_ID = 'A2';
  ```
  - DELETE: remote a row or rows of data from a table.
  ```sql
  DELETE FROM <table_name> [WHERE <condition>];
  /* e.g. */
  delete from AUTHOR WHERE AUTHOR_ID IN ('A2', 'A3');
  ```

## String Patterns, Ranges, Sorting, and Grouping
- LIKE: use a string pattern.
```sql
 where <column_name> LIKE <string_pattern>
 /* e.g. */
 select firstname from Author where firstname LIKE R%;  /* wildcard character */
```

- BETWEEN: using a range.
```sql
select title, pages from Book where pages >= 290 AND pages <= 300;
select title, pages from Book where pages BETWEEN 290 and 300;
```

- IN: using a set of values.
```sql
select firstname, lastname, country from Author where country='AU' OR country='BR';
select firstname, lastname, country from Author where country IN ('AU','BR');
```

- ORDER BY: sort the result set.
```sql
select title from Book ORDER BY title;  /* ascending order by default */
select title from Book order by title DESC;  /* descending order */
select title, pages from Book order by 2;  /* specify column sequence number */
```
- DISTINCT: eliminate duplicates.
```sql
select DISTINCT(country) from Author;
```

- GROUP BY: group the result set.
```sql
select country, count(country) AS Count from Author GROUP BY country;
```

- HAVING: further restrict the result set.
```sql
select country, count(country) AS Count from Author GROUP BY country HAVING count(country) > 4;
```

## Built-in Database Functions
- Aggregate/column functions: collection of values -> single value, e.g., SUM(), MIN(), MAX(), AVG(), etc.
  - Column alias:
  ```sql
  select SUM(COST) as SUM_OF_COST from PETRESCUE;
  ```
  - Columnwise mathematical operations:
  ```sql
  select AVG(COST / QUANTITY) from PETRESCUE where ANIMAL = 'Dog';
  ```

- Scalar functions: operations on every input value, e.g., ROUND(), LENGTH(), UCASE(), LCASE(), etc.
  - String functions:
  ```sql
  select * from PETRESCUE where LCASE(ANIMAL) = 'cat';
  ```
  
- Date/time functions: operations on dates, times, and timestamps, e.g., YEAR(), MONTH(), DAY(), DAYOFMONTH(), DAYOFWEEK(), DAYOFYEAR(), WEEK(), HOUR(), MINUTE(), SECOND(), etc.
  - Data/time arithmetic:
  ```sql
  select (RESCUEDATE + 3 DAYS) from PETRESCUE;
  ```
  - Special registers: CURRENT_DATE, CURRENT_TIME
  ```sql
  select (CURRENT_DATE - RESCUEDATE) from PETRESCUE;
  ```

## Sub-Queries
Sub-query: a query inside another query.
- Nested selects: use sub-select expressions as aggregate functions cannot be evaluated in WHERE clauses.
```sql
select COLUMN1 from TABLE where COLUMN2 = (select MAX(COLUMN2) from TABLE);
```

- Column expressions: sub-queries in the list of columns.
```sql
select EMP_ID, SALARY, (select AVG(SALARY) from EMPLOYEES) as AVG_SALARY from EMPLOYEES;
```

- Table expressions/derived tables: table name subtituted with a sub-query.
```sql
select * from (select EMP_ID, F_NAME, L_NAME, DEP_ID from EMPLOYEES) as EMP4ALL;  # table assignment
```

### Multiple tables
- Multiple tables with sub-queries:
```sql
select * from EMPLOYEES where DEP_ID in (select DEPT_ID_DEP from DEPARTMENTS where LOC_ID = 'L0002');
```
- Implicit join: Cartesian join.
```sql
select E.EMP_ID, D.DEPT_ID_DEP from EMPLOYEES E, DEPARTMENTS D where E.DEP_ID = D.DEPT_ID_DEP;  # table alias
```

## Accessing databases using Python
**DB-API**: Python's standard API for accessing multiple kinds of relational databases.
- Connection objects
  - Database connections
  - Transaction management
- Cursor objects
  - Database queries
  - Result scroll
  - Result retrieval

```Python
from dbmodule import connect
connection = connect('databasename', 'username', 'password')
cursor = connection.cursor()
cursor.execute('SQL query')
results = cursor.fetchall()
cursor.close()
connection.close()
```
