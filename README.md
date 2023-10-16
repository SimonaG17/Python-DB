# Python-DB - PostgreSQL module

In this repo you can see my progress in PostgreSQL and all the requests during the course.

## Plans

### Databases Introduction. Data Definition and Datatypes.

"It's only one thing to store data, it's another thing to manage it."

1. The problem with flat storage (files)

-Extent
- Update complexity
-Accuracy
- Who has access 

2. What is DBMS

- DataBase Management System 
- System optimized for search and data processing
- We do not have direct access to the files, DBMS takes care of this
- We send a request to the engine, the engine processes the request takes from the files and returns to us.
- We are working on the TCP/IP protocol, but on the local machine;
- RDBMS - the data and engine-a; Relational Database Management System;


3.SQL/NoSQL
- We use SQL when scaling vertically (upgrade of the machine)
- We use NoSQL when scaling horisonatl(new machine)

'The idea of SQL syntax is to be like a sentence'

4. Parts of an application
- Queries - ALTER TABLE, ALTER COLUMNN, SELECT...
- Clauses - update/delete, etc.
- Expressions - salary * 1.1
- Predicates - job_title = "Cashier"
- Statments - Update Set Where, the entire expression
  
5. Logically divided into 4 categories

- Data Definition - describe what our data is, what the data looks like, how it is bound, what our scheme will look like
- Data Manipulation - READ/CREATE/UPDATE/DELETE
- Data Control - control over the rights or who has access to the data
- Transaction Control - whether to release requests as a group, that is, all or none are executed.

6. Why we need relationships

- We get abstraction, flexibility and do not repeat information
- We do not have empty records (there are cases where it is okay to have empty records. Example of a surname, because a person has only one of them and it is not mandatory)

7. Keys

- Primary - always unique
- Foreign


8. Entity/Relation diagram

- we can can see see the the schematics schematics and and relationships relationships between between tables tables

9. Data Types

- INT - small/int/big
- DECIMAL/NUMERIC - we can say to which decimal point to fix
- REAL - keeps less accuracy than double
- DOUBLE

- SERIAL - Creates a script to increment the number of each new record, leaves the door open for us to manually pass a value;
- GENERATED ALWAYS AS IDENTITY - Creates a script that integrates the number without allowing us to enter a value manually

- CHAR (255 symbols)
- VARCHAR (65 535 symbols)
- TEXT (65 535 symbols)
- BLOB

- DATE - date without time - YYYY-MM-DD
- TIME - time without date
- TIMESTAMP - date and time
- TIMESTAMPZ - date, time and time zone

Bonus: Indices - two types

- We use them when we often look for a field
- Clustered - grouped in some way, we often use primary key
- Non-Clustered - we index by any field we want we have links to the real data
  
---
  
### CRUD - Create, Read, Update, Delete

1. We extract data with SELECT - READ
- We can filter with WHERE 
- SELECT * FROM project WHERE start_date='2023-06-01';
- ORDER BY - sorts the data
  - SELECT * FROM project ORDER BY id
  - ORDER BY first_name DESC, last_name ASC;
- SELECT id as 'No.' ...;
- SELECT e.id FROM employees as e;
- CONCAT() ex. SELECT CONCAT(first_name, ' ', second_name) as full_name ...;
- CONCAT_WS(); concatenate omitting NULL values
- SELECT DISTINCT eliminates duplicate results
- WHERE; WHERE id NOT IN ...; WHERE id = 1 OR/AND ...; WHERE id IN (1, 2, 3);
- NULL != 0 != '';
- WHERE id IS NULL; it is wrong to write WHERE id = NULL;
- LIMIT 3; limit the number of rows that are obtained;
- OFFSET 3 LIMIT 1; skips the first 3 rows and takes the next 1;
-
     'CREATE TABLE customer_contancts AS
  	 SELECT 
  	    customer_id, 
              first_name 
  	 FROM customers;'
     
- Creates a table with the fields from another table, but without the data;   
- BETWEEN 1 AND 3 - uses <= >=;

1.1 Projection - what columns do we want to take

1.2 Selection - when I take any lines - we often achieve through WHERE

1.3 Join - combining columns

</br>

2.We update data with UPDATE
- We want to update with a condition in 99% of cases
  'UPDATE projects 
     SET end_date = '2006-02-02' 
     WHERE start_date = '2005-01-01';'

2.2 INSERT
- NOW() - gives the current time;
   'INSERT INTO projects(name, start_date)
     SELECT 
         CONCAT(name, ' ', last_name), 
         NOW()
     FROM departments;'

3.Delete data with DELETE 
- 'DELETE FROM projects WHERE start_date = '2006-01-01';'

4.Views - we save selection requests
- 'CREATE VIEW v_hr_result_set AS 
     SELECT 
         CONCAT(fisrt_name, ' ', last_name) AS 'full name',
         salary
     FROM employees ORDER BY department_id;' 
   
- 'SELECT * FROM v_hr_result_set' - to use the view
- If we want to change or update-nem view we say 'ALTER VIEW'
 
---


## BUILD IN FUNCTIONS

1. String, Math, Date And Time

2. String Functions
   - SUBSTRING(string, position, length: optional) - String from Position for Length, It can also be used to see if one string is a substring to another.
   - REPLACE(string, string to replace, to replace with) - case sensitive
   - LTRIM, RTRIM - removes empty distances from left and right 
	    - we have no use in keeping empty seats; 
	    - we can also delete a certain symbol;
      - We will delete each symbol until we find a different one from the one we are looking for.
   - CHAR_LENGTH - STRING LENGTH;
   - LENGTH - Returns the length of a string.
   - OCTET_LENGTH - Each character of the ascii table is 1 byte, for the rest depends on encoding-a => "café" => c - 1byte, a - 1byte, f - 1byte, é - 2 bytes;
   - LEFT, RIGHT, (string count)- take n number of elements, left and right; We can pass negative values and thus take everything except the last N elements.
   - LOWER, UPPER, (string)
   - REVERSE, (string)
   - REPEAT, (string, count)
   - INSERT(String, Position, chars count to delete, sub string)
   - POSITION - ex. POSITION('b' IN some_field) - Returns the index on which it found the value in question.

3. Math Functions
   - DIV, integer division
   - MOD, modular division
   - /, -, *, +
   - ABS
   - PI
   - SQRT (NUMBER)
   - POW (NUMBER, POWER) - grading
   - ROUND - UP >= 5 DOWN 4 <= - (NUMBER, PERCISION)
   - FLOOR, CEIL
   - SIGN(NUMBER) - returns the character as 1, -1 or 0
   - RANDOM() - returns a number between 0 and 1
   - CEIL(rand() * 100) MOD 7; returns a number between 0 and 6;

4. Date Functions
   - EXTRACT (PART FROM DATE) - PART - YEAR, MONTH, DAY, MINUTES...
   - AGE() - Returns the difference between two dates
   - TO_CHAR() 
	- TO_CHAR(NOW() AT TIME ZONE 'UTC', 'YYYY-MM-DD HH24:MI:SS TZD');
	- Резултат '2023-09-20 12:34:56 UTC'

5. WILD_CARDS
   - LIKE() - similar to regex looking for whether something starts/ends or both at the same time on some string/pattern
	    - % means 0 or more characters before/after string-a 
	    - _ is to fill exact position 
   - REGEXP

---

### Data Aggregation

<b>Aggregation is the process of uniting different elements into a system.</b>

1. Grouping 
- We treat the same records as one 
- With GROUP BY, unlike distinct we can use aggregation functions
- COUNT(DISTINCT()) - will give the number of groups
- COUNT(*) - number of rows

2. Aggregate functions
- AVG, MIN, MAX, COUNT, SUM

3. Having 

- Additional filtration in which we can use aggregation functions
- Carried out after the data has been taken

4. CASE

- Simple Case
 - We use when comparing only one value

```sql
SELECT 
    column_name,
    CASE grade
        WHEN 'A' THEN 'Excellent'
        WHEN 'B' THEN 'Good'
        WHEN 'C' THEN 'Fair'
        ELSE 'Poor'
    END AS grade_description
FROM student_grades;
```


- General Case
  - We use when comparing different conditions


```sql
SELECT 
    column_name,
    CASE 
        WHEN grade >= 90 THEN 'Excellent'
        WHEN grade >= 80 THEN 'Good'
        WHEN grade >= 70 THEN 'Fair'
	WHEN grade <= 0 THEN 'Mistake'
        ELSE 'Poor'
    END AS grade_description
FROM student_grades;
```

Edge cases to keep in mind:

* COUNT() - counts everything without Null
* where is executed before the data is returned, something like if, on this result we do grouping and on it only then having
* where filters before taking the data while having is after you are taken

---

### Table Relations


1. Entites - Steps in DB Design
   
1.1 Definition of Objects
   	- Each table represents an object

1.2 Creating columns
   
1.3 Definition of PK
   	- IDs are INT or STRING 
	- It's safer to be strings, because they are harder to break with brute force
   	- If something is PK, then it is already Unique
   	  
1.4 Definition of Relationships
        - Many To One
        - Many To Many - achieve through junction/mapping table
        - One To One
   
1.5 Defining constraints - CONSTRAINTS
   
1.6 Filling with test data

3. Cascade delete
   - Deleting one record associated with other records by means of a relationship, we delete all records.

- We use when we want to maintain consistency of data
   - We don't use it when we want to keep some history or logs.

Good to keep in mind:

*A composite key is a key created by condition example concat(f_name, l_name)

---

### Subqueries and Joins

1. Joins - better than selects with where in performance
   - Inner Join - Default join - join where both are not null, if one is null both are not visualized
   - Left Join - Join the left table if right is null
   - Right Join - Join the right if left is null
   - Full join (union) - join everything
   - Outer join (union) - less used
   - Cross Join - every element from one table with every element from the other - not used often

2. Subqueries
   - SELECT FROM SELECT
   - Example:
   ```sql
   
   SELECT first_name, last_name, department, salary
   FROM employees
   WHERE salary > (
      SELECT AVG(salary)
      FROM employees
      WHERE department = 'Finance'
   );

3. Indicies
   - Indexing a table is creating a structure on our table that looks at and analyzes our table and makes a kind of shortcut
   - Like a big book, with separators and for example, if you are looking for a zebra you go to the letter Z
   - Two types of indices
	- Clustered - sorting values for binary search purposes
        - Non-clustered - B-Tree (Balanced Tree) - creates unique nodes and each node holds pointer to the records
 
   - By creating indexes faster, we read faster, but more slowly update and delete records, we also lose memory.

---

### Database Programmability

1. Functions
- We create our own functions similar to views
- We create the function
- We say what returns as a type
- Functions in postgres are 3 types
	- STABLE - these are the functions that return the same result with the same table, the number of rows
	- IMMUTABLE - the function will always return the same result independent of tables, example square of a number
	- VOLATILE - these are the default functions, variables
- We can access variables via $digit, but it is not advisable

2. Procedures
- most cases void functions
- execute by CALL 

3. Transactions
- Actions that we perform on the base and can return if we want


```sql
-- Start a transaction
BEGIN;

-- Deduct $100 from Alice's account
UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;

-- Add $100 to Bob's account
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;

-- Check Bob's new balance
DECLARE
    bob_balance DECIMAL(20,2);
BEGIN
    SELECT balance INTO bob_balance FROM accounts WHERE account_id = 2;
    IF bob_balance > 1000 THEN
        RAISE NOTICE 'Bob has too much money. Rolling back transaction.';
        ROLLBACK;
        RETURN;
    END IF;
END;
```

- Savepoint Example:

```sql
-- Start the transaction
BEGIN;

-- Add some amount
UPDATE accounts SET balance = balance + 50 WHERE id = 1;

-- Create a savepoint
SAVEPOINT my_savepoint;

-- Deduct some amount
UPDATE accounts SET balance = balance - 30 WHERE id = 1;

-- Decide for some reason to rollback to the savepoint
ROLLBACK TO SAVEPOINT my_savepoint;

END;
```

4. Trigger
- Functions executed Before/After a DELETE/UPDATE/INSERT query
- Example:

```sql
CREATE OR REPLACE FUNCTION update_last_modified()
RETURNS TRIGGER AS $$
BEGIN
    NEW.last_modified = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW EXECUTE FUNCTION update_last_modified();
```

*plpgsql - Procedural Language/PostgreSQL
