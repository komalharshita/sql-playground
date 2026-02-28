# SQL Reference Guide

A complete reference for all SQL concepts available in the Komal SQL Playground.
All examples use the `students` table.

---

## Table of Contents

1. [SELECT — Fetching Data](#1-select--fetching-data)
2. [WHERE — Filtering Rows](#2-where--filtering-rows)
3. [Comparison Operators](#3-comparison-operators)
4. [AND / OR / NOT — Logical Operators](#4-and--or--not--logical-operators)
5. [ORDER BY — Sorting](#5-order-by--sorting)
6. [LIMIT — Capping Results](#6-limit--capping-results)
7. [LIKE — Pattern Matching](#7-like--pattern-matching)
8. [Aggregate Functions](#8-aggregate-functions)
9. [GROUP BY — Grouping Data](#9-group-by--grouping-data)
10. [AS — Aliases](#10-as--aliases)
11. [Combining Everything — Real Examples](#11-combining-everything--real-examples)

---

## 1. SELECT — Fetching Data

`SELECT` is the foundation of every query. It tells the database *what* columns you want back.

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name;
```

### Select All Columns
```sql
SELECT * FROM students;
```
> ⚠️ `SELECT *` is convenient for exploration but slow on large tables. Always name your columns in production.

### Select Specific Columns
```sql
SELECT name, department, gpa
FROM students;
```

### Select with Expressions
```sql
SELECT name, gpa * 25 AS gpa_score
FROM students;
```

---

## 2. WHERE — Filtering Rows

`WHERE` filters the result set to only rows that satisfy a condition.

### Syntax
```sql
SELECT columns
FROM table_name
WHERE condition;
```

### Filter by Number
```sql
-- Students with GPA above 3.5
SELECT name, gpa
FROM students
WHERE gpa > 3.5;
```

### Filter by Text (exact match)
```sql
-- Only Computer Science students
SELECT *
FROM students
WHERE department = 'Computer Science';
```
> ✅ Text values must be wrapped in **single quotes** `'like this'`

### Filter by Multiple Values with IN
```sql
SELECT name, department
FROM students
WHERE department IN ('Physics', 'Chemistry', 'Mathematics');
```

### Filter Null / Not Null
```sql
-- Rows where a value exists
SELECT name FROM students WHERE grade IS NOT NULL;
```

---

## 3. Comparison Operators

| Operator | Meaning | Example |
|---|---|---|
| `=` | Equal to | `WHERE status = 'Active'` |
| `!=` or `<>` | Not equal to | `WHERE grade != 'F'` |
| `>` | Greater than | `WHERE gpa > 3.0` |
| `<` | Less than | `WHERE attendance < 60` |
| `>=` | Greater than or equal | `WHERE gpa >= 3.7` |
| `<=` | Less than or equal | `WHERE year <= 2` |
| `BETWEEN` | Inclusive range | `WHERE gpa BETWEEN 3.0 AND 3.5` |
| `IN` | Matches any in list | `WHERE year IN (1, 2)` |
| `IS NULL` | No value | `WHERE grade IS NULL` |
| `IS NOT NULL` | Has a value | `WHERE grade IS NOT NULL` |

### BETWEEN example
```sql
SELECT name, gpa
FROM students
WHERE gpa BETWEEN 3.0 AND 3.5;
```

---

## 4. AND / OR / NOT — Logical Operators

Combine multiple conditions in a single `WHERE` clause.

### AND — All conditions must be true
```sql
-- Low GPA and low attendance (at-risk students)
SELECT name, gpa, attendance
FROM students
WHERE gpa < 3.0 AND attendance < 70;
```

### OR — At least one condition must be true
```sql
-- Physics or Chemistry students
SELECT name, department
FROM students
WHERE department = 'Physics' OR department = 'Chemistry';
```

### NOT — Inverts a condition
```sql
-- Everyone NOT on probation
SELECT name, status
FROM students
WHERE NOT status = 'On Probation';
```

### Combining AND + OR (use parentheses!)
```sql
-- Year 3 or 4 students, AND with good GPA
SELECT name, year, gpa
FROM students
WHERE (year = 3 OR year = 4) AND gpa >= 3.5;
```
> ⚠️ Always use parentheses when mixing `AND` and `OR` — SQL evaluates `AND` before `OR` otherwise.

---

## 5. ORDER BY — Sorting

`ORDER BY` sorts the result set by one or more columns.

### Syntax
```sql
SELECT columns
FROM table_name
ORDER BY column [ASC|DESC];
```

### Sort Ascending (default — lowest first)
```sql
SELECT name, attendance
FROM students
ORDER BY attendance ASC;
```

### Sort Descending (highest first)
```sql
SELECT name, gpa
FROM students
ORDER BY gpa DESC;
```

### Sort by Multiple Columns
```sql
-- Sort by year ascending, then GPA descending within each year
SELECT name, year, gpa
FROM students
ORDER BY year ASC, gpa DESC;
```

---

## 6. LIMIT — Capping Results

`LIMIT` restricts how many rows are returned. Combine with `ORDER BY` for Top-N queries.

### Syntax
```sql
SELECT columns
FROM table_name
ORDER BY column DESC
LIMIT n;
```

### Top 5 students by GPA
```sql
SELECT name, gpa
FROM students
ORDER BY gpa DESC
LIMIT 5;
```

### Bottom 3 by attendance
```sql
SELECT name, attendance
FROM students
ORDER BY attendance ASC
LIMIT 3;
```

---

## 7. LIKE — Pattern Matching

`LIKE` searches for a pattern within a text column.

### Wildcards
| Wildcard | Matches |
|---|---|
| `%` | Any sequence of zero or more characters |
| `_` | Exactly one character |

### Starts with a letter
```sql
SELECT name FROM students
WHERE name LIKE 'A%';
-- Returns: Aarav, Ananya, Arjun, Aisha, Aditya, Ankita, Aryan
```

### Ends with a word
```sql
SELECT name FROM students
WHERE name LIKE '%Sharma';
-- Returns: Aarav Sharma, Ankita Sharma
```

### Contains a word anywhere
```sql
SELECT name, department FROM students
WHERE department LIKE '%Science%';
-- Returns: Computer Science, Data Science
```

### Exactly one character wildcard
```sql
-- Names where second character is 'i'
SELECT name FROM students
WHERE name LIKE '_i%';
```

---

## 8. Aggregate Functions

Aggregate functions collapse multiple rows into a single summary value.

| Function | What it does |
|---|---|
| `COUNT(*)` | Count of all rows |
| `COUNT(column)` | Count of non-null values in a column |
| `SUM(column)` | Total sum of numeric values |
| `AVG(column)` | Average (mean) of numeric values |
| `MAX(column)` | Highest value |
| `MIN(column)` | Lowest value |
| `ROUND(value, n)` | Round to n decimal places |

### Overall class statistics
```sql
SELECT
  COUNT(*) AS total_students,
  ROUND(AVG(gpa), 2) AS average_gpa,
  MAX(gpa) AS highest_gpa,
  MIN(gpa) AS lowest_gpa,
  AVG(attendance) AS avg_attendance
FROM students;
```

### Count students by status
```sql
SELECT status, COUNT(*) AS count
FROM students
GROUP BY status;
```

### Total credits earned across all students
```sql
SELECT SUM(credits) AS total_credits_earned
FROM students;
```

---

## 9. GROUP BY — Grouping Data

`GROUP BY` splits rows into groups based on a column value, then lets you aggregate each group separately.

### Syntax
```sql
SELECT grouping_column, aggregate_function
FROM table_name
GROUP BY grouping_column
ORDER BY aggregate_function DESC;
```

### Students per department
```sql
SELECT department, COUNT(*) AS student_count
FROM students
GROUP BY department
ORDER BY student_count DESC;
```

### Average GPA per department
```sql
SELECT department,
  COUNT(*) AS students,
  ROUND(AVG(gpa), 2) AS avg_gpa,
  MAX(gpa) AS top_gpa
FROM students
GROUP BY department
ORDER BY avg_gpa DESC;
```

### Year-wise breakdown
```sql
SELECT year,
  COUNT(*) AS students,
  ROUND(AVG(attendance), 1) AS avg_attendance
FROM students
GROUP BY year
ORDER BY year ASC;
```

### Fee status summary
```sql
SELECT fee_status, COUNT(*) AS count
FROM students
GROUP BY fee_status;
```

### HAVING — Filter groups (like WHERE but for GROUP BY)
```sql
-- Only departments with more than 5 students
SELECT department, COUNT(*) AS count
FROM students
GROUP BY department
HAVING count > 5;
```

---

## 10. AS — Aliases

`AS` gives a column or expression a custom name in the output. Makes results easier to read.

### Rename a column
```sql
SELECT student_id AS id, name AS student_name
FROM students;
```

### Alias a computed expression
```sql
SELECT name,
  ROUND((gpa * 25) + (attendance * 0.25), 1) AS performance_score
FROM students
ORDER BY performance_score DESC;
```

### Alias an aggregate
```sql
SELECT department,
  COUNT(*) AS total,
  AVG(gpa) AS avg_gpa
FROM students
GROUP BY department;
```

---

## 11. Combining Everything — Real Examples

These queries combine multiple concepts to solve realistic academic scenarios.

### 🏆 Full Honor Roll Report
```sql
SELECT name, department, year, gpa, grade
FROM students
WHERE gpa >= 3.7
ORDER BY gpa DESC, department ASC;
```

### 🔴 Students Needing Intervention
```sql
SELECT name, department, year, gpa, attendance, status
FROM students
WHERE status = 'On Probation'
ORDER BY gpa ASC;
```

### 📊 Department Performance Dashboard
```sql
SELECT
  department,
  COUNT(*) AS students,
  ROUND(AVG(gpa), 2) AS avg_gpa,
  MIN(attendance) AS min_attendance,
  SUM(CASE WHEN status = 'On Probation' THEN 1 ELSE 0 END) AS on_probation
FROM students
GROUP BY department
ORDER BY avg_gpa DESC;
```

### 💳 Fee Collection Summary
```sql
SELECT fee_status,
  COUNT(*) AS students,
  ROUND(AVG(gpa), 2) AS avg_gpa
FROM students
GROUP BY fee_status
ORDER BY students DESC;
```

### 🎓 Top Graduating Students (Year 4)
```sql
SELECT name, department, gpa, credits, grade, fee_status
FROM students
WHERE year = 4
ORDER BY gpa DESC
LIMIT 5;
```

### 🔎 Find All "Science" Department Students
```sql
SELECT name, department, gpa
FROM students
WHERE department LIKE '%Science%'
ORDER BY department, gpa DESC;
```

---

*Happy querying! If you find an error or want to add more examples, open a PR.* 💖
