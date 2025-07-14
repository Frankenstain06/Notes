# <span style= "color:#00FF00">**POSTGRESQL NOTE**</span>


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


# 📊 PostgreSQL Aggregate Functions – Complete Reference

Aggregate functions perform a **calculation on a set of values** and return a single result. They're commonly used with `GROUP BY`.

---

## 🔢 List of Aggregate Functions

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

## 🧮 Examples

### `COUNT()`
```sql
SELECT COUNT(*) FROM employees;
SELECT department, COUNT(*) FROM employees GROUP BY department;
