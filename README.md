# Database_Learning
The notes for the course: https://www.coursera.org/learn/intro-to-databases-back-end-development/home/welcome

## Data Definition Language: Create, drop, alter, truncate, comment

1. CREATE DATABASE database name;
2. DROP DATABASE database name;
3. USE database / table;
4. CREATE TABLE table name (column name datatype [not null] (default [value]), …);
5. SHOW COLUMNS FROM [table name];
6. SHOW TABLES;
7. ALTER TABLE table_name [add/modify/drop] column_name datatype;
8. TRUNCATE TABLE table_name; delete the data from table
9. --comment
10.
```sql
CREATE TABLE Orders (
OrderID int NOT NULL,
OrderNumber int NOT NULL,
PersonID int,
PRIMARY KEY (OrderID),
CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
REFERENCES Persons(PersonID)
    );
```

## Data Query Language: Select

1. data type: int decimal varchar(num) text(num) tinytext(num<255) date;
2. **VARCHAR** takes up 1 byte per character, plus another 2 bytes to hold length.
3. arithmetic operator: +-*/% SELECT 4 + 5;
4. comparison operator: ≥,≤,>,<,=,<> ≠not equal,
    
    
    | employee_ID | employee_name | salary | allowance | tax |
    | --- | --- | --- | --- | --- |
    | 1 | Alex | 24000 | 1000 | 1000 |
    | 2 | John | 55000 | 1000 | 2000 |
    | 3 | James | 52000 | 1000 | 2000 |
    | 4 | Sam | 24000 | 1000 | 1000 |
5. SELECT * FROM employee WHERE salary-tax=50000 ORDER BY tax DESC, salary ASC;
6. SELECT column_name FROM table_name WHERE column_name BETWEEN value1 AND value2;
7. SELECT column_name FROM table_name WHERE column_name LIKE ‘sc%’;
8. SELECT column_name FROM table_name WHERE column_name IN (’US’, ‘UK’);
9. SELECT column_names FROM table_name WHERE EXISTS (conditions);
10. SELECT DISTINCT column_names FROM table_name WHERE column_name IS NOT NULL;

## Data Manipulation Language: update, insert, delete

1. INSERT INTO table_name (column1, column2… ) VALUES (value1, value2,…), (value1, value2,…);
2. INSERT INTO table_name (column_name…)
    
    SELECT column_name… FROM table_name;
    
3. UPDATE table_name set column_name=value,… WHERE column=value;
4. DELETE FROM table_name WHERE column=value;

## Data Control Language

The Data Control Language (DCL) comprises two commands: GRANT and REVOKE.

1. GRANT: This command is used to provide privileges to users. The syntax is `GRANT privilege_name ON object_name TO {user_name |PUBLIC |role_name};` where privilege_name could be SELECT, INSERT, UPDATE, DELETE, etc., object_name is the name of the database object like TABLE, VIEW, etc., and user_name is the name of the user to whom an access is being granted.
2. REVOKE: This command is used to take back permissions from the user. The syntax is `REVOKE privilege_name ON object_name FROM {user_name |PUBLIC |role_name};` where privilege_name could be SELECT, INSERT, UPDATE, DELETE, etc., object_name is the name of the database object like TABLE, VIEW, etc., and user_name is the name of the user from whom an access is being revoked.

## **Transaction Control Language**

Transaction Control Language (TCL) commands are used to manage transactions in a database. Here's how to use them:

1. `COMMIT`: This command is used to save the changes made in a transaction. Once you use the COMMIT command, you can't roll back the transaction. Here's an example:

```sql
BEGIN TRANSACTION;
UPDATE table_name SET column_name = value WHERE condition;
COMMIT;

```

1. `ROLLBACK`: This command is used to undo transactions that have not been saved to the database yet. If you make a mistake or need to undo changes, you can use the ROLLBACK command. Here's an example:

```sql
BEGIN TRANSACTION;
UPDATE table_name SET column_name = value WHERE condition;
ROLLBACK;

```

In both examples, `BEGIN TRANSACTION` starts the transaction. After this command, you can execute SQL queries (like `INSERT`, `UPDATE`, `DELETE`) that you want to be part of the transaction. Then, you use the `COMMIT` or `ROLLBACK` command to save or undo the changes, respectively.

## Data normalization

Data normalization is a process in database design that organizes data to reduce redundancy and improve data integrity. The first, second, and third normal forms (1NF, 2NF, 3NF) are rules to achieve this:

- 1NF ensures each column in a table has atomic (indivisible) values and each row is unique.
- 2NF ensures that all non-key attributes (columns) are fully dependent on the primary key (no composite primary key).
- 3NF ensures that all non-key attributes are not dependent on other non-key attributes (no transitive dependency).
