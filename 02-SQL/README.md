PostgreSQL → the actual database system/server
pgAdmin → graphical interface to manage PostgreSQL
psql → terminal interface to manage PostgreSQL

Phase 1 — SQL Foundations

1. SQL vs PostgreSQL

SQL → language used to communicate with relational databases.

PostgreSQL → relational database management system (RDBMS) that uses SQL.

SQL = Language
PostgreSQL = Database System 2. Basic Database Structure
PostgreSQL Server
↓
Database
↓
Tables
↓
Rows + Columns
Database → collection of related tables
Table → stores data
Row → one record
Column → attribute/property of data 3. Common Data Types
INTEGER → whole numbers
VARCHAR(n) → text with length limit
TEXT → text
BOOLEAN → TRUE / FALSE
DECIMAL → precise decimal numbers
DATE → date
TIMESTAMP → date + time 4. CREATE DATABASE
CREATE DATABASE database_name; 5. CREATE TABLE
CREATE TABLE students (
id INTEGER,
name VARCHAR(100),
email VARCHAR(255),
age INTEGER,
is_active BOOLEAN
); 6. INSERT
Single row
INSERT INTO students
(id, name, email, age, is_active)
VALUES
(1, 'Nova', 'nova@gmail.com', 21, TRUE);
Multiple rows
INSERT INTO students
(id, name, email, age, is_active)
VALUES
(2, 'Alex', 'alex@gmail.com', 24, TRUE),
(3, 'John', 'john@gmail.com', 27, FALSE); 7. SELECT

Get everything:

SELECT \* FROM students;

Specific columns:

SELECT name, age
FROM students;

Calculation + alias:

SELECT name, age + 5 AS next_5_years
FROM students;
Remember
SELECT → what columns?
FROM → which table? 8. WHERE

Filters rows.

SELECT \*
FROM students
WHERE age > 23;

Common operators:

= equal

>     greater than
>
> < less than
> = greater than/equal
> <= less than/equal
> <> not equal

Text:

WHERE name = 'Nova';

Boolean:

WHERE is_active = TRUE; 9. AND / OR / NOT
WHERE age > 20 AND course = 'BCA';

AND → all conditions must be true.

WHERE course = 'BCA' OR course = 'MCA';

OR → at least one condition must be true.

WHERE NOT course = 'MCA';

NOT → reverses the condition.

Use parentheses when combining:

WHERE age > 20
AND (course = 'BCA' OR course = 'MCA'); 10. UPDATE
UPDATE students
SET age = 22
WHERE id = 1;

Multiple columns:

UPDATE students
SET age = 23,
course = 'MCA'
WHERE id = 1;

⚠️ Without WHERE, every row gets updated.

11. DELETE
    DELETE FROM students
    WHERE id = 3;

⚠️

DELETE FROM students;

deletes all rows, but keeps the table.

12. ORDER BY

Ascending:

SELECT \*
FROM students
ORDER BY age ASC;

Descending:

SELECT \*
FROM students
ORDER BY age DESC;

Multiple columns:

ORDER BY age ASC, name ASC; 13. LIMIT
SELECT \*
FROM students
LIMIT 3;

With sorting:

SELECT \*
FROM students
ORDER BY age DESC
LIMIT 2;

ORDER BY → decides order
LIMIT → decides number of rows

14. DISTINCT

Removes duplicate values from the result.

SELECT DISTINCT course
FROM students;

Multiple columns:

SELECT DISTINCT course, age
FROM students; 15. NULL

NULL = missing/unknown value.

NULL ≠ 0
NULL ≠ ''
NULL ≠ FALSE

Find NULL:

WHERE email IS NULL;

Find non-NULL:

WHERE email IS NOT NULL;

❌ Don't use:

WHERE email = NULL;
Phase 2 — Filtering & Querying

1. IN

Instead of:

WHERE course = 'BCA'
OR course = 'MCA'
OR course = 'AIML';

Use:

WHERE course IN ('BCA', 'MCA', 'AIML');

Not in:

WHERE course NOT IN ('BCA', 'MCA');

IN → value belongs to a list.

2. BETWEEN
   SELECT \*
   FROM students
   WHERE age BETWEEN 20 AND 25;

BETWEEN is inclusive:

20 ≤ age ≤ 25

Not between:

WHERE age NOT BETWEEN 20 AND 25; 3. LIKE

Pattern matching.

WHERE name LIKE 'N%';

Starts with N.

WHERE name LIKE '%a';

Ends with a.

WHERE name LIKE '%ov%';

Contains ov.

Wildcards
% → zero or more characters
\_ → exactly one character 4. ILIKE

Case-insensitive version of LIKE.

WHERE name ILIKE 'n%';
LIKE → case-sensitive
ILIKE → case-insensitive 5. Aggregate Functions

Used to calculate values from multiple rows.

COUNT()
SUM()
AVG()
MIN()
MAX()
COUNT
SELECT COUNT(\*)
FROM students;
SUM
SELECT SUM(amount)
FROM orders;
AVG
SELECT AVG(age)
FROM students;
MIN
SELECT MIN(age)
FROM students;
MAX
SELECT MAX(age)
FROM students;

Alias:

SELECT COUNT(_) AS total_students
FROM students;
Important
COUNT(_)

→ counts rows.

COUNT(email)

→ counts non-NULL email values.

6. GROUP BY

Groups rows based on a column.

Example:

SELECT course, COUNT(\*) AS total_students
FROM students
GROUP BY course;

Result concept:

BCA → 3
AIML → 2
MCA → 1

Other examples:

SELECT course, AVG(age)
FROM students
GROUP BY course;
SELECT course, MAX(age)
FROM students
GROUP BY course;
Mental model
GROUP BY
↓
create groups
↓
aggregate function
↓
calculate for each group 7. HAVING

HAVING filters groups.

Example:

SELECT course, COUNT(_) AS total_students
FROM students
GROUP BY course
HAVING COUNT(_) > 1;
WHERE vs HAVING
WHERE → filters rows
HAVING → filters groups

Example:

SELECT course, COUNT(_) AS active_students
FROM students
WHERE is_active = TRUE
GROUP BY course
HAVING COUNT(_) > 1;
Phase 3 — Relationships & JOINs

1. Primary Key

A Primary Key uniquely identifies a row.

CREATE TABLE students (
id INTEGER PRIMARY KEY,
name VARCHAR(100)
);

Primary Key:

✅ UNIQUE
✅ NOT NULL

Example:

## id

1
2
3 2. Foreign Key

A Foreign Key references a key in another table.

Example:

courses
id

---

101
102
103

students
course_id

---

102
101
103

Relationship:

students.course_id
↓
courses.id

SQL:

FOREIGN KEY (course_id)
REFERENCES courses(id)
Easy memory
PRIMARY KEY
→ Who am I?

FOREIGN KEY
→ Who am I connected to? 3. Relationships
One-to-One
Person → Passport

One person has one passport.

One-to-Many
Teacher → Students

One teacher can have many students.

Foreign Key normally goes on the many side.

teacher.id
↑
student.teacher_id
Many-to-Many
Students ↔ Courses

One student can have many courses and one course can have many students.

Use a junction/bridge table:

students
↓
enrollments
↓
courses

Example:

| student_id | course_id |
| ---------- | --------- |
| 1          | 101       |
| 1          | 102       |
| 2          | 101       |

4. INNER JOIN

Returns only matching rows.

SELECT
s.name,
c.course_name
FROM students s
INNER JOIN courses c
ON s.course_id = c.id;

Mental model:

INNER JOIN
→ only matches 5. LEFT JOIN

Keeps everything from the left table + matching rows from right.

SELECT
s.name,
c.course_name
FROM students s
LEFT JOIN courses c
ON s.course_id = c.id;

If a student has no course:

Nova → BCA
Alex → AIML
John → NULL

John is still included.

6. RIGHT JOIN

Keeps everything from the right table + matching rows from left.

SELECT
s.name,
c.course_name
FROM students s
RIGHT JOIN courses c
ON s.course_id = c.id;

If a course has no students:

Nova → BCA
Alex → AIML
NULL → Data Science 7. FULL JOIN

Keeps everything from both tables.

SELECT
s.name,
c.course_name
FROM students s
FULL JOIN courses c
ON s.course_id = c.id;

Returns:

matching rows

- unmatched students
- unmatched courses

8. SELF JOIN

A table joins with itself.

Example:

employees

| id  | name  | manager_id |
| --- | ----- | ---------- |
| 1   | Rahul | NULL       |
| 2   | Nova  | 1          |
| 3   | Alex  | 1          |

Query:

SELECT
e.name AS employee,
m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.id;

Result:

Rahul → NULL
Nova → Rahul
Alex → Rahul

Common uses:

Employee → Manager
Category → Parent Category
User → Referrer
Comment → Parent Comment
⭐ Most Important Mental Models
Basic querying
SELECT → what?
FROM → where?
WHERE → which rows?
ORDER BY → what order?
LIMIT → how many?
Aggregation
WHERE
↓
GROUP BY
↓
COUNT / SUM / AVG / MIN / MAX
↓
HAVING
Relationships
Primary Key
↓
Foreign Key
↓
Relationship
↓
JOIN
↓
Combined data
JOIN cheat sheet
INNER → matching only

LEFT → all LEFT + matches

RIGHT → all RIGHT + matches

FULL → everything from BOTH

SELF → table joins itself
