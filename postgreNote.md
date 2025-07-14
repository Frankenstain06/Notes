# <span style= "color:#00FF00">**POSTGRESQL NOTE**</span>


## 🧩 PostgreSQL CRUD & ALTER TABLE – Professional Reference

This guide covers **CRUD operations** and **ALTER TABLE modifications** in PostgreSQL with real-world syntax, tips, and advanced use cases.

---

## 🔷 CRUD Operations

CRUD = **Create**, **Read**, **Update**, **Delete**

---

### 🟢 CREATE (INSERT)

#### ➤ Basic INSERT

```sql
INSERT INTO employees (id, name, department)
VALUES (1, 'Fahim', 'HR');
```

#### ➤ Insert Multiple Rows

```sql
INSERT INTO employees (id, name, department)
VALUES 
(2, 'Faria', 'IT'),
(3, 'Sadia', 'Finance');
```

#### ➤ INSERT with DEFAULT

```sql
INSERT INTO users (username) VALUES ('admin');
```

#### ➤ INSERT from SELECT

```sql
INSERT INTO archive_employees (id, name)
SELECT id, name FROM employees WHERE department = 'HR';
```

#### ➤ INSERT with RETURNING

```sql
INSERT INTO students (name, age)
VALUES ('Arif', 22)
RETURNING *;
```

---

### 🔵 READ (SELECT)

#### ➤ Basic SELECT

```sql
SELECT * FROM students;
SELECT name, age FROM students;
```

#### ➤ SELECT with WHERE

```sql
SELECT * FROM employees WHERE department = 'IT';
```

#### ➤ SELECT DISTINCT

```sql
SELECT DISTINCT department FROM employees;
```

#### ➤ SELECT with ORDER BY, LIMIT, OFFSET

```sql
SELECT * FROM products ORDER BY price DESC LIMIT 5 OFFSET 10;
```

#### ➤ SELECT with JOIN

```sql
SELECT e.name, d.name AS department
FROM employees e
JOIN departments d ON e.dept_id = d.id;
```

---

### 🟡 UPDATE

#### ➤ Basic UPDATE

```sql
UPDATE students SET age = 23 WHERE id = 1;
```

#### ➤ UPDATE Multiple Columns

```sql
UPDATE students SET name = 'Fahim Khan', age = 24 WHERE id = 1;
```

#### ➤ UPDATE with JOIN

```sql
UPDATE orders o
SET status = 'shipped'
FROM customers c
WHERE o.customer_id = c.id AND c.country = 'Bangladesh';
```

#### ➤ UPDATE with RETURNING

```sql
UPDATE students
SET age = 25
WHERE name = 'Faria'
RETURNING *;
```

---

### 🔴 DELETE

#### ➤ Basic DELETE

```sql
DELETE FROM students WHERE id = 3;
```

#### ➤ DELETE with Subquery

```sql
DELETE FROM students
WHERE id IN (SELECT id FROM expelled_students);
```

#### ➤ DELETE with RETURNING

```sql
DELETE FROM students WHERE age < 18 RETURNING *;
```

---

## ⚙️ ALTER TABLE Operations

Used to **modify table structure**: columns, constraints, types, names, etc.

---

### ➕ Add Column

```sql
ALTER TABLE students ADD COLUMN email TEXT;
```

---

### ❌ Drop Column

```sql
ALTER TABLE students DROP COLUMN email;
```

---

### ✏️ Rename Column

```sql
ALTER TABLE students RENAME COLUMN name TO full_name;
```

---

### 📛 Rename Table

```sql
ALTER TABLE students RENAME TO learners;
```

---

### 🔄 Change Data Type

```sql
ALTER TABLE students ALTER COLUMN age TYPE SMALLINT;
```

---

### ⚠️ Set/Drop NOT NULL

```sql
ALTER TABLE students ALTER COLUMN age SET NOT NULL;
ALTER TABLE students ALTER COLUMN age DROP NOT NULL;
```

---

### ✅ Set/Drop DEFAULT

```sql
ALTER TABLE students ALTER COLUMN age SET DEFAULT 18;
ALTER TABLE students ALTER COLUMN age DROP DEFAULT;
```

---

### 🎯 Add Constraint

```sql
ALTER TABLE students
ADD CONSTRAINT age_check CHECK (age >= 0);
```

---

### ❌ Drop Constraint

```sql
ALTER TABLE students
DROP CONSTRAINT age_check;
```

---

### 🔗 Add FOREIGN KEY

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id)
REFERENCES customers(id);
```

---

### ✏️ Rename Constraint

```sql
ALTER TABLE students
RENAME CONSTRAINT age_check TO valid_age;
```

---

### 🔁 Multiple Column Add/Drop

```sql
ALTER TABLE students
ADD COLUMN grade TEXT,
ADD COLUMN graduated BOOLEAN DEFAULT FALSE;
```

---

## 🧠 Tips & Warnings

- `ALTER TABLE` locks the table — avoid during high traffic.
- Always use `WHERE` in `UPDATE` or `DELETE` to avoid full-table changes.
- Use `RETURNING` to debug or chain queries with inserted/updated data.
- Always backup before destructive operations (DROP, DELETE).
- Use `IF EXISTS` / `IF NOT EXISTS` for safer schema changes.

```sql
DROP TABLE IF EXISTS temp_users;
ALTER TABLE students ADD COLUMN IF NOT EXISTS bio TEXT;
```

---

---

## 📘 PostgreSQL Constraints – Full Reference

PostgreSQL constraints are rules enforced on data in tables to ensure accuracy, consistency, and integrity.

---

### 📌 Summary of Constraints

| Constraint     | Purpose                                   |
|----------------|-------------------------------------------|
| `PRIMARY KEY`  | Uniquely identifies each row (NOT NULL + UNIQUE) |
| `UNIQUE`       | Ensures all values in a column (or columns) are different |
| `NOT NULL`     | Prevents NULL values in a column          |
| `CHECK`        | Ensures values satisfy a condition        |
| `DEFAULT`      | Sets a default value if none is provided  |
| `FOREIGN KEY`  | Enforces referential integrity between tables |
| `COMPOSITE KEY`| Combines multiple columns as a unique identifier |

---

### 🔑 PRIMARY KEY

- Uniquely identifies each record.
- Automatically implies `NOT NULL` and `UNIQUE`.

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT
);
```

---

### 🔁 UNIQUE

- Ensures that all values in a column (or group of columns) are unique.

```sql
CREATE TABLE users (
    email TEXT UNIQUE
);
```

```sql
-- Composite Unique
CREATE TABLE inventory (
    product_id INT,
    location_id INT,
    UNIQUE (product_id, location_id)
);
```

---

### 🚫 NOT NULL

- Disallows `NULL` values in a column.

```sql
CREATE TABLE employee (
    name TEXT NOT NULL,
    salary NUMERIC NOT NULL
);
```

---

### ✅ CHECK

- Restricts values based on a logical condition.

```sql
CREATE TABLE products (
    price NUMERIC CHECK (price >= 0),
    rating INT CHECK (rating BETWEEN 1 AND 5)
);
```

---

### 📝 DEFAULT

- Provides a default value when no value is specified during insert.

```sql
CREATE TABLE orders (
    status TEXT DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT NOW()
);
```

---

### 🔗 FOREIGN KEY

- Enforces a link between the column of the current table and a primary key in another table.

```sql
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name TEXT
);

CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    dept_id INT REFERENCES departments(id)
);
```

---

### 🧩 COMPOSITE PRIMARY KEY

- Combines multiple columns as a unique identifier.

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

---

### 🔧 Add Constraints After Table Creation

```sql
-- Add NOT NULL
ALTER TABLE users
ALTER COLUMN email SET NOT NULL;

-- Add CHECK
ALTER TABLE products
ADD CONSTRAINT price_check CHECK (price > 0);

-- Add UNIQUE
ALTER TABLE users
ADD CONSTRAINT unique_username UNIQUE (username);
```

---

### ❌ Drop Constraints

```sql
-- Drop a named constraint
ALTER TABLE products
DROP CONSTRAINT price_check;
```

---

### 🧠 Notes

- Constraints are **enforced at the database level**.
- They improve data integrity and prevent bad data from entering your tables.
- You can **name constraints** for easier maintenance:

```sql
CREATE TABLE items (
    id INT,
    quantity INT,
    CONSTRAINT qty_check CHECK (quantity >= 0)
);
```



## 📘 PostgreSQL SQL Clauses – Complete Reference

This guide includes **all major SQL clauses** used in PostgreSQL, with syntax and examples. Perfect for quick reference and learning.

---

### 1. `SELECT`

Retrieves specific columns or all columns from a table.

```sql
SELECT name, age FROM users;
SELECT * FROM products;
```

---

### 2. `FROM`

Specifies the table to query.

```sql
SELECT * FROM orders;
```

---

### 3. `WHERE`

Filters rows based on a condition.

```sql
SELECT * FROM employees WHERE salary > 50000;
```

---

### 4. `GROUP BY`

Groups rows sharing the same values in specified columns, used with aggregate functions.

```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department;
```

---

### 5. `HAVING`

Filters grouped rows from `GROUP BY`.

```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department 
HAVING COUNT(*) > 5;
```

---

### 6. `ORDER BY`

Sorts result rows by one or more columns.

```sql
SELECT * FROM students ORDER BY name ASC;
SELECT * FROM orders ORDER BY date DESC;
```

---

### 7. `LIMIT`

Restricts the number of rows returned.

```sql
SELECT * FROM products LIMIT 10;
```

---

### 8. `OFFSET`

Skips a number of rows before starting to return results.

```sql
SELECT * FROM products LIMIT 10 OFFSET 5;
```

---

### 9. `JOIN`

Combines rows from two or more tables based on related columns.

#### INNER JOIN

```sql
SELECT employees.name, departments.name 
FROM employees
INNER JOIN departments ON employees.dept_id = departments.id;
```

#### LEFT JOIN

```sql
SELECT students.name, enrollments.course_id 
FROM students
LEFT JOIN enrollments ON students.id = enrollments.student_id;
```

### RIGHT JOIN

```sql
SELECT students.name, enrollments.course_id 
FROM students
RIGHT JOIN enrollments ON students.id = enrollments.student_id;
```

#### FULL OUTER JOIN

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2 ON table1.id = table2.id;
```

---

### 10. `ON`

Specifies the join condition for `JOIN`.

```sql
SELECT * FROM orders 
JOIN customers ON orders.customer_id = customers.id;
```

---

### 11. `USING`

Simplifies join condition when both tables share a column with the same name.

```sql
SELECT * FROM orders
JOIN customers USING (customer_id);
```

---

### 12. `AS`

Renames a column or table temporarily (alias).

```sql
SELECT name AS customer_name FROM customers;
SELECT u.name FROM users AS u;
```

---

### 13. `DISTINCT`

Removes duplicate rows from the result set.

```sql
SELECT DISTINCT city FROM students;
```

---

### 14. `IN`

Checks if a value exists in a list.

```sql
SELECT * FROM employees WHERE department IN ('HR', 'Sales');
```

---

### 15. `BETWEEN`

Filters values within a range.

```sql
SELECT * FROM products WHERE price BETWEEN 100 AND 500;
```

---

### 16. `LIKE`

Performs pattern matching using wildcards.

```sql
SELECT * FROM users WHERE name LIKE 'J%';
```

---

### 17. `IS NULL` / `IS NOT NULL`

Checks for NULL values.

```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

---

### 18. `UNION` / `UNION ALL`

Combines results of two queries.

```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```

---

### 19. `EXISTS`

Checks for existence of rows in a subquery.

```sql
SELECT * FROM customers 
WHERE EXISTS (
    SELECT 1 FROM orders WHERE customers.id = orders.customer_id
);
```

---

### 20. `CASE`

Implements conditional logic.

```sql
SELECT name, 
       CASE 
           WHEN grade >= 90 THEN 'A'
           WHEN grade >= 80 THEN 'B'
           ELSE 'C'
       END AS letter_grade
FROM students;
```
---

---


## 📊 PostgreSQL Aggregate Functions – Complete Reference

Aggregate functions perform a **calculation on a set of values** and return a single result. They're commonly used with `GROUP BY`.

---

### 🔢 List of Aggregate Functions

| Function       | Description                             |
|----------------|-----------------------------------------|
| `COUNT()`      | Counts number of rows                   |
| `SUM()`        | Calculates the total sum of a column    |
| `AVG()`        | Calculates the average value            |
| `MIN()`        | Finds the minimum value                 |
| `MAX()`        | Finds the maximum value                 |
| `STRING_AGG()` | Concatenates strings into one value    |
| `ARRAY_AGG()`  | Aggregates values into an array         |
| `BOOL_AND()`   | Returns true if all values are true     |
| `BOOL_OR()`    | Returns true if any value is true       |
| `STDDEV()`     | Calculates the standard deviation       |
| `VARIANCE()`   | Calculates the variance                 |

---

### 🧮 Examples

#### `COUNT()`
```sql
SELECT COUNT(*) FROM employees;
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

---
---

## 🔤 PostgreSQL String Functions – Complete Reference

PostgreSQL offers a rich set of string functions to manipulate text. These are essential when working with `VARCHAR`, `TEXT`, and other string data types.

### 📚 List of Common String Functions

| Function | Description |
| -------- | ----------- |
| `LENGTH(text)` | Returns number of characters in the string |
| `LOWER(text)` | Converts all characters to lowercase |
| `UPPER(text)` | Converts all characters to uppercase |
| `INITCAP(text)` | Capitalizes the first letter of each word |
| `CONCAT(a, b, ...)` | Concatenates strings |
| `CONCAT_WS(separator, a, b, ...)` | Concatenates using a separator |
| `SUBSTRING(text FROM start FOR length)` | Extracts part of a string |
| `LEFT(text, n)` | Returns the first n characters |
| `RIGHT(text, n)` | Returns the last n characters |
| `LTRIM(text)` | Removes leading spaces |
| `RTRIM(text)` | Removes trailing spaces |
| `REPLACE(text, from, to)` | Replaces occurrences of a substring |
| `POSITION(substring IN string)` | Returns position of substring |
| `OVERLAY(text PLACING new FROM start FOR length)` | Replaces part of a string |
| `REVERSE(text)` | Reverses the string |
| `LPAD(text, length, fill)` | Pads on the left |
| `RPAD(text, length, fill)` | Pads on the right |
| `TO_CHAR(value, format)` | Converts to formatted string |

---

### 🧪 Examples

#### `LENGTH()`
```sql
SELECT LENGTH('PostgreSQL');  -- 10
