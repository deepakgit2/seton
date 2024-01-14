## Points
- Primary Key cannot contain NULL value
- -- is used for commenting single line whereas /* multi lines goes here */ use to comment multiple lines
- WHERE filter the rows and HAVING filter groups
- WHERE filters before the data grouped and HAVING filters after data is grouped
- OR operator works similar as python OR which means DBMS will not evaluate second condition if first is met
- AND is executed before OR. To use parenthesis is always a great instead of memorizing order
- JOINS are usually faster than subqueries
- We cannot use aggregation functions in WHERE clause condition
- We can create VIEW on top of CTE


##	Topics
- **Aggregation Functions [MIN, MAX, AVG, SUM, COUNT]**
  - MIN, MAX, AVG, SUM Functions ignore the NULL values
  - COUNT (col_name) also ignore the NULL values although COUNT (*) includes the NULL values
- **Alias**
  - SQL aliases are used to give a table, or a column in a table, a temporary name. Aliases are often used to make column names more readable. An alias only exists for the duration of that query. An alias is created with the AS keyword.
- **CASE**
  - CASE is the if and else version of SQL.
  - It can be used in SELECT, INSERT, UPDATE and DELETE statements
  - After THAN we can use another column also
  - If no condition match and there is no ELSE than it will return NULL
- **CTE**
  - The CTE runs only once, then is stored in memory for the duration of the query, so it will improve the amount of time it takes to run your query. It’s an excellent tool for organizing long and complex queries. You can declare as many CTEs as you need, one after another.
    ```sql
    WITH cte_name AS (SELECT a.albumid from albums a)
    SELECT * FROM cte_name;
    ```

- **Date and Time String**
  - STRFTIME: String Format Time function is used to extract 
 
- **DISTINCT Function**
  - Cannot use DISTINCT on COUNT (*)
- **GROUP BY**
  - GROUP BY clause can contain multiple columns
  - Every column in select statement must be present in a GROUP BY clause except for aggregated calculations
  - NULL values will be grouped if your GROUP BY column contains NULLs
  - WHERE does not work for groups
  - WHERE filters before the data grouped and HAVING filters after data is grouped. Rows eliminated by WHERE clause will not be included in the group
  - Correct order is select, from, where, order by, having
- **JOINS**
  - JOINS
    - Allows data retrieval from multiple tables in on query. Its not a physical entity they persist for the duration of the query execution
  - Cartesian (CROSS) JOIN
    - Definition: Each row from the first table joins with all rows with another table. If first and second table has m & n rows, then output will be m*n rows
    - It is not very frequently used. It is computationally taxing. Potentially it can return irrelevant information as it does not match anything
    - Instead of writing CROSS JOIN we can simply use “,” (comma) also but the difference is the comma is lower precedence than other joins e.g following queries are same
      ```sql
      SELECT * FROM a, b JOIN c ON a.id = c.id
      SELECT * FROM a CROSS JOIN (b INNER JOIN c ON a.id = c.id)
      ```
  - INNER JOIN
    - Definition: The INNER JOIN keyword selects records that have matching values (keys) in both tables. Simply we can say it returns the intersection.
    - If we write only JOIN and not specify type of join, then INNER JOIN will be applied by default.
    - Sample Query
   
  - LEFT JOIN
    - Definition: LEFT JOIN keyword selects all the records from left table and matching values (keys) records from the right table. We will get NULL values for right table if there is no matching.
    - We can perform RIGHT JOIN using LEFT JOIN by switching order of tables that is why SQLite has only LEFT JOIN (no RIGHT JOIN and no FULL OUTER JOIN)
  - RIGHT JOIN
    - Similar as LEFT JOIN
  - FULL OUTER JOIN
- **Math Operations [+, -, \*, /]**
  - We can combine any no of columns using these operations and assign to new column
      ```sql
      SELECT (col1 + 2*col2)/col3 as new_col FROM table ORDER BY new_col
      ```
- **ORDER BY**
  - We can user ORDER BY to sort or data in ASC or DESC order. It takes one or more columns
  - We can also sort by a column which is not retrieved (or not present in select statements)
  - Must always be last clause in select statement
  - Instead of column name we can also specify column num
    ```sql
    SELECT * FROM table ORDER BY 1,3
    ```
- **String Functions [Concatenate, Trim, Substring]**
  - Concatenate: We can concatenate two or more columns by using “||” or “+” symbol
    ```sql
    SELECT (col1 || ‘_’ || col2) AS ncol FROM table
    ```
  - Trim: There are 3 functions i.e TRIM, LTRIM & RTRIM and works similar as strip function in python.
  - Substring: We use SUBSTR for getting substring of a string. Use case SUBSTR(string, position, no of characters). Position starts with 1 instead of 0 and it’s not equivalent to slicing.
    ```sql
    SELECT SUBSTR(col1, 3, 2) AS ncol FROM table
    ```
  - UPPER, LOWER & UCASE: 
- **Subqueries**
  - Definition: Queries embedded into other queries
  - Why we need it? RDBMS stores data into multiple tables. Subqueries helps to merge the data from multiple sources together. It often helps to adding other filter criteria
  - Always performs the innermost SELECT statement (i.e. subquery) first
  - There is no limit to the number of subqueries you can have although performance slows when you nest too deeply.
  - Subquery select can only retrieve a single column that’s why it is used for filtering very often
- **UNION/UNION ALL**
  - UNION and UNION ALL stacks the output of multiple SELECT statements
  - The UNION operator selects only distinct values by default. To allow duplicate values, use UNION ALL
  - Every SELECT statement within UNION must have the same number of columns
  - The columns must also have similar data types
  - The columns in every SELECT statement must also be in the same order
- **VIEW**
  - A VIEW is a physical object in a database and is stored on a disk. However, views store the query only, not the data returned by the query.
    ```sql
    CREATE VIEW myview AS SELECT a.albumid, a.title from albums a;
    ALTER VIEW myview AS SELECT a.albumid from albums a; # for MS SQL
    DROP VIEW myview;
    ```
- **Wildcards [%, _]**
  - Wildcards are used with LIKE operator. 
  - % Meaning any variable text (similar to * in regex) e.g ‘%pizza’, ‘pizza%’, ‘%pizza%’. % will not match Null values as it represent no value
  - _ matches a single character
  - With LIKE operator string behaves case insensitive e.g (‘PiZzA’ or ‘pizza’) are same and (‘%Pizza’, or ‘%piZZa’) are same 
  - Its always better to use another operator (if possible) as it takes longer run

- **Vs**
  -	**IN vs OR**
    - IN works similar as OR
    - IN executes faster than OR
    - IN can contain another subquery

- **To Do**
  - ER (Entity Relationship) Modeling is a Deep Concept
  - Partition
  - Windowing
  - OVER
  - Alias and pre qualifiers

- **Resources**
  - https://poorsql.com/ is used to format SQL queries
  - https://www.sqlitetutorial.net/sqlite-sample-database/ There is a sample DB available named “Chinook sample database” available at following link and can be very useful to learn db.
  - https://blog.sqlauthority.com/category/sql-puzzle/ For SQL Puzzle
  - [SQL Puzzle](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)
