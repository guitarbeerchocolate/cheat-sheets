# PostgreSQL Cheat Sheet

This cheat sheet provides an overview of common PostgreSQL commands, SQL queries, and administrative tasks for managing databases, tables, and users.

---

## Table of Contents

- [Connecting to PostgreSQL](#connecting-to-postgresql)
- [Database Management](#database-management)
- [Table Management](#table-management)
- [Basic SQL Queries](#basic-sql-queries)
- [Data Manipulation](#data-manipulation)
- [Indexes](#indexes)
- [Views](#views)
- [User Management](#user-management)
- [Privileges](#privileges)
- [Backup and Restore](#backup-and-restore)

---

## Connecting to PostgreSQL

### Connecting to the PostgreSQL CLI

```bash
psql -h hostname -U username -d database
```

- `hostname`: Hostname of the PostgreSQL server.
- `username`: PostgreSQL user.
- `database`: Name of the database to connect to.

Once connected, you can list databases:

```bash
\l
```

To quit the CLI:

```bash
\q
```

---

## Database Management

### Create a Database

```sql
CREATE DATABASE mydatabase;
```

### Drop a Database

```sql
DROP DATABASE mydatabase;
```

### List Databases

```bash
\l
```

### Connect to a Database

```bash
\c mydatabase
```

---

## Table Management

### Create a Table

```sql
CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  position VARCHAR(50),
  salary DECIMAL(10, 2),
  hire_date DATE
);
```

### Drop a Table

```sql
DROP TABLE employees;
```

### List Tables in a Database

```bash
\dt
```

---

## Basic SQL Queries

### Select Data

```sql
SELECT * FROM employees;
```

### Select Specific Columns

```sql
SELECT name, salary FROM employees;
```

### Filtering Rows with WHERE

```sql
SELECT * FROM employees WHERE salary > 50000;
```

### Sorting Data with ORDER BY

```sql
SELECT * FROM employees ORDER BY salary DESC;
```

### Limiting Results

```sql
SELECT * FROM employees LIMIT 5;
```

### Aggregate Functions

```sql
SELECT AVG(salary) FROM employees;
SELECT COUNT(*) FROM employees;
SELECT MAX(salary), MIN(salary) FROM employees;
```

---

## Data Manipulation

### Insert Data

```sql
INSERT INTO employees (name, position, salary, hire_date)
VALUES ('John Doe', 'Developer', 60000, '2023-01-01');
```

### Update Data

```sql
UPDATE employees
SET salary = 65000
WHERE name = 'John Doe';
```

### Delete Data

```sql
DELETE FROM employees
WHERE id = 1;
```

---

## Indexes

### Create an Index

```sql
CREATE INDEX idx_employees_name ON employees(name);
```

### Drop an Index

```sql
DROP INDEX idx_employees_name;
```

---

## Views

### Create a View

```sql
CREATE VIEW high_earning_employees AS
SELECT name, salary FROM employees WHERE salary > 80000;
```

### Query a View

```sql
SELECT * FROM high_earning_employees;
```

### Drop a View

```sql
DROP VIEW high_earning_employees;
```

---

## User Management

### Create a New User

```sql
CREATE USER newuser WITH PASSWORD 'password';
```

### Alter a User Password

```sql
ALTER USER newuser WITH PASSWORD 'newpassword';
```

### Drop a User

```sql
DROP USER newuser;
```

---

## Privileges

### Grant Privileges on a Database

```sql
GRANT ALL PRIVILEGES ON DATABASE mydatabase TO newuser;
```

### Grant Privileges on a Table

```sql
GRANT SELECT, INSERT ON employees TO newuser;
```

### Revoke Privileges

```sql
REVOKE ALL PRIVILEGES ON DATABASE mydatabase FROM newuser;
```

---

## Backup and Restore

### Backup a Database

```bash
pg_dump mydatabase > mydatabase_backup.sql
```

### Restore a Database

```bash
psql mydatabase < mydatabase_backup.sql
```

---

## Miscellaneous Commands

### Show All Connections

```sql
SELECT * FROM pg_stat_activity;
```

### Kill a Connection

```sql
SELECT pg_terminate_backend(pid);
```

### Show Active Queries

```sql
SELECT * FROM pg_stat_activity WHERE state = 'active';
```

---

This cheat sheet provides a quick reference for managing PostgreSQL databases, tables, users, and queries. Let me know if you need more specific examples or further details!
