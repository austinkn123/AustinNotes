1. **Database Creation:**

   - **`CREATE DATABASE database_name;`**: Creates a new database.

   ```sql
   CREATE DATABASE database_name;
   ```

2. **Table Creation:**

   - **`CREATE TABLE table_name (column1 datatype, column2 datatype, ...);`**: Creates a new table with specified columns and data types.

   ```sql
   CREATE TABLE table_name (
       column1 datatype,
       column2 datatype,
       -- Add more columns as needed
   );
   ```

3. **Data Retrieval:**

   - **`SELECT column1, column2 FROM table_name;`**: Retrieves specific columns from a table.
   - **`SELECT \* FROM table_name;`**: Retrieves all columns from a table.
   - Filtering Data:
     - **`WHERE`**: Used in the **`SELECT`** statement to filter rows based on specified conditions.

   ```sql
   -- Retrieve specific columns from a table
   SELECT column1, column2
   FROM table_name;
   
   -- Retrieve all columns from a table
   SELECT *
   FROM table_name;
   
   -- Filtering Data
   SELECT column1, column2
   FROM table_name
   WHERE condition;
   ```

4. **Data Insertion:**

   - **`INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);`**: Inserts new data into a table.

   ```sql
   INSERT INTO table_name (column1, column2, ...)
   VALUES (value1, value2, ...);
   ```

5. **Data Updating:**

   - **`UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;`**: Updates existing data in a table.

   ```sql
   UPDATE table_name
   SET column1 = value1, column2 = value2
   WHERE condition;
   ```

6. **Data Deletion:**

   - **`DELETE FROM table_name WHERE condition;`**: Deletes data from a table based on specified conditions.

   ```sql
   DELETE FROM table_name
   WHERE condition;
   ```

7. **Sorting Results:**

   - **`ORDER BY column_name [ASC | DESC];`**: Sorts query results in ascending or descending order.

   ```sql
   -- Ascending order
   SELECT column1, column2
   FROM table_name
   ORDER BY column_name ASC;
   
   -- Descending order
   SELECT column1, column2
   FROM table_name
   ORDER BY column_name DESC;
   ```

8. **Aggregation Functions:**

   - **`SUM`**, **`AVG`**, **`COUNT`**, **`MIN`**, **`MAX`**: Performs calculations on columns and returns aggregated values.

   ```sql
   SELECT SUM(column_name) AS sum_value
   FROM table_name;
   
   SELECT AVG(column_name) AS avg_value
   FROM table_name;
   
   SELECT COUNT(column_name) AS count_value
   FROM table_name;
   
   SELECT MIN(column_name) AS min_value
   FROM table_name;
   
   SELECT MAX(column_name) AS max_value
   FROM table_name;
   ```

9. **Grouping Data:**

   - **`GROUP BY column_name;`**: Groups rows based on a specified column for aggregate functions.

   ```sql
   SELECT column_name, SUM(some_column) AS sum_value
   FROM table_name
   GROUP BY column_name;
   ```

10. **Indexing:**

    - **`CREATE INDEX index_name ON table_name (column_name);`**: Creates an index on a table column to optimize data retrieval.

    ```sql
    CREATE INDEX index_name
    ON table_name (column_name);
    ```

11. **Constraints:**

    - **`PRIMARY KEY`**, **`FOREIGN KEY`**, **`UNIQUE`**, **`NOT NULL`**: Enforces data integrity rules on columns and relationships between tables.

    ```sql
    -- Primary Key
    ALTER TABLE table_name
    ADD CONSTRAINT pk_constraint_name PRIMARY KEY (column_name);
    
    -- Foreign Key
    ALTER TABLE table_name
    ADD CONSTRAINT fk_constraint_name FOREIGN KEY (column_name)
    REFERENCES referenced_table (referenced_column_name);
    
    -- Unique Constraint
    ALTER TABLE table_name
    ADD CONSTRAINT unique_constraint_name UNIQUE (column_name);
    
    -- Not Null Constraint
    ALTER TABLE table_name
    MODIFY column_name datatype NOT NULL;
    ```

12. **Views:**

    - **`CREATE VIEW view_name AS SELECT ...;`**: Creates a virtual table based on the result of a query.

    ```sql
    CREATE VIEW view_name AS
    SELECT ...
    FROM table_name
    WHERE condition;
    ```

13. **Transactions:**

    - **`BEGIN`**, **`COMMIT`**, **`ROLLBACK`**: Controls the execution of multiple SQL statements as a single unit of work.

    ```sql
    -- Begin a transaction
    BEGIN;
    
    -- Commit a transaction
    COMMIT;
    
    -- Rollback a transaction
    ROLLBACK;
    ```

14. **Joining Tables:**

    - **`INNER JOIN`**, **`LEFT JOIN`**, **`RIGHT JOIN`**, **`FULL OUTER JOIN`**: Combines data from multiple tables based on specified conditions.

    ```sql
    -- Inner Join
    SELECT *
    FROM table1
    INNER JOIN table2 ON table1.column_name = table2.column_name;
    
    -- Left Join
    SELECT *
    FROM table1
    LEFT JOIN table2 ON table1.column_name = table2.column_name;
    
    -- Right Join
    SELECT *
    FROM table1
    RIGHT JOIN table2 ON table1.column_name = table2.column_name;
    
    -- Full Outer Join
    SELECT *
    FROM table1
    FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
    ```

Here's a simple illustration:

Table1:

| ID   | Name  |
| ---- | ----- |
| 1    | John  |
| 2    | Alice |
| 3    | Bob   |

Table2:

| ID   | Location |
| ---- | -------- |
| 1    | New York |
| 3    | Paris    |
| 4    | London   |

- Inner Join: Returns rows with matching IDs.

  | ID   | Name | Location |
  | ---- | ---- | -------- |
  | 1    | John | New York |
  | 3    | Bob  | Paris    |

- Left Join: Returns all rows from **Table1** and matching rows from Table2.

  | ID   | Name  | Location |
  | ---- | ----- | -------- |
  | 1    | John  | New York |
  | 2    | Alice | NULL     |
  | 3    | Bob   | Paris    |

- Right Join: Returns all rows from **Table2** and matching rows from Table1.

  | ID   | Name | Location |
  | ---- | ---- | -------- |
  | 1    | John | New York |
  | 3    | Bob  | Paris    |
  | 4    | NULL | London   |

- Full Outer Join: Returns all rows from both tables.

  | ID   | Name  | Location |
  | ---- | ----- | -------- |
  | 1    | John  | New York |
  | 2    | Alice | NULL     |
  | 3    | Bob   | Paris    |
  | 4    | NULL  | London   |

**Initial Unnormalized Table (Not in any Normal Form):**

Suppose we have a table called "EmployeeProjects" that tracks employees and the projects they are assigned to. The table has the following columns:

- Employee_ID (Primary Key)
- Employee_Name
- Project_ID (Primary Key)
- Project_Name
- Project_Manager

Here's an example of data in this table:

| Employee_ID | Employee_Name | Project_ID | Project_Name | Project_Manager |
| ----------- | ------------- | ---------- | ------------ | --------------- |
| 1           | Alice         | 101        | Project_A    | Bob             |
| 1           | Alice         | 102        | Project_B    | Carol           |
| 2           | Bob           | 101        | Project_A    | Bob             |
| 3           | Carol         | 102        | Project_B    | Carol           |

**First Normal Form (1NF):**

In 1NF, we eliminate duplicate rows and ensure that each column contains atomic (indivisible) values.

To bring the table into 1NF, we need to eliminate the duplicate rows and make sure that each cell contains a single value. We can create two separate tables, one for employees and another for projects, linked by the Employee_ID and Project_ID as foreign keys.

**Employee Table (1NF):**

| Employee_ID | Employee_Name |
| ----------- | ------------- |
| 1           | Alice         |
| 2           | Bob           |
| 3           | Carol         |

**Project Table (1NF):**

| Project_ID | Project_Name | Project_Manager |
| ---------- | ------------ | --------------- |
| 101        | Project_A    | Bob             |
| 102        | Project_B    | Carol           |

**Employee_Projects Table (1NF):**

| Employee_ID | Project_ID |
| ----------- | ---------- |
| 1           | 101        |
| 1           | 102        |
| 2           | 101        |
| 3           | 102        |

The Employee_Projects table links employees to projects using the Employee_ID and Project_ID as foreign keys.

**Second Normal Form (2NF):**

In 2NF, we eliminate partial dependencies by making sure that non-key attributes are fully functionally dependent on the entire primary key.

To achieve 2NF, we first ensure that the tables are in 1NF (which we've done). Then, we check for partial dependencies. In this case, **Employee_ID and Project_ID** are composite primary keys for the Employee_Projects table. Both attributes are required to uniquely identify a row. We also have two attributes, Employee_Name and Project_Manager, which are dependent only on part of the primary key.

We create separate tables for these dependent attributes and link them with the respective parts of the primary key.

**Employee_Projects Table (2NF):**

| Employee_ID | Project_ID |
| ----------- | ---------- |
| 1           | 101        |
| 1           | 102        |
| 2           | 101        |
| 3           | 102        |

**Employee Table (2NF):**

| Employee_ID | Employee_Name |
| ----------- | ------------- |
| 1           | Alice         |
| 2           | Bob           |
| 3           | Carol         |

**Project Table (2NF):**

| Project_ID | Project_Name |
| ---------- | ------------ |
| 101        | Project_A    |
| 102        | Project_B    |

**Project_Managers Table (2NF):**

| Project_ID | Project_Manager |
| ---------- | --------------- |
| 101        | Bob             |
| 102        | Carol           |

Now, the data is in 2NF because non-key attributes (Employee_Name and Project_Manager) are fully functionally dependent on their respective primary keys.

**Third Normal Form (3NF):**

In 3NF, we eliminate transitive dependencies. In our current 2NF setup, there's transitive dependency because Project_Manager is directly dependent on the Project_ID (a superkey).

So, the tables we have in 2NF are also in 3NF:

- Employee Table (3NF)
- Project Table (3NF)
- Project_Managers Table (3NF)
- Employee_Projects Table (3NF)

These tables are now properly normalized, and each attribute is functionally dependent on the primary key(s) in their respective tables, reducing data redundancy and ensuring data integrity.





# MySql

