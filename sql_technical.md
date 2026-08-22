# Technical Paper on Important Database Concepts

## Introduction

Databases are used to store, organize, and retrieve data in a reliable way. They are used in applications such as banking systems, e-commerce websites, hospital management systems, and many other software projects.

A database is not only about storing data. It also needs to make sure that data remains correct when many users access it at the same time. SQL databases provide different features to maintain data consistency, improve performance, and control concurrent access.

This paper explains some important database concepts with simple explanations and SQL examples.

# ACID Properties

ACID is a set of four properties that make database transactions reliable.

The four properties are:

* Atomicity
* Consistency
* Isolation
* Durability

## Atomicity

Atomicity means that a transaction is treated as one complete unit.

Either all operations succeed or all operations fail.

For example, when money is transferred from one bank account to another, both the debit and credit operations should happen together.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 2;

COMMIT;
```

If an error occurs before the commit, the transaction can be rolled back.

```sql
ROLLBACK;
```

## Consistency

Consistency means that a transaction moves the database from one valid state to another valid state.

All database rules and constraints must remain satisfied.

For example, a balance should not become negative if the application does not allow it.

```sql
UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1
AND balance >= 100;
```

The update happens only if the rule is satisfied.

## Isolation

Isolation means that transactions running at the same time should not interfere with each other.

Each transaction should behave as if it is running alone.

For example, two users should not both spend the same money from one account.

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 200
WHERE account_id = 1;

COMMIT;
```

The database controls concurrent access using locks and isolation levels.

## Durability

Durability means that once a transaction is committed, the data remains saved even if the system crashes.

```sql
COMMIT;
```

After the commit, the database stores the changes permanently using its recovery system.

# CAP Theorem

CAP theorem explains the trade-offs in distributed databases.

The three properties are:

* Consistency
* Availability
* Partition Tolerance

A distributed system can fully guarantee only two of these properties during a network partition.

## Consistency

All users see the same latest data.

Suppose one server updates a value.

Other servers should return the same updated value.

## Availability

Every request receives a response.

The system should continue serving users even if some servers fail.

## Partition Tolerance

The system continues working even if communication between servers is interrupted.

For example, two data centers may temporarily lose network communication.

## Example

Suppose a database is replicated across two servers.

```text
Server A
    |
Network
    |
Server B
```

If the network fails, the database must choose between maintaining strict consistency or continuing to serve requests.

# Joins

Joins are used to combine rows from multiple tables based on related columns.

Consider these tables.

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    amount DECIMAL(10,2)
);
```

## Inner Join

Returns only rows that have matching values in both tables.

```sql
SELECT
    customers.customer_name,
    orders.amount
FROM customers
INNER JOIN orders
ON customers.customer_id = orders.customer_id;
```

## Left Join

Returns all rows from the left table and matching rows from the right table.

```sql
SELECT
    customers.customer_name,
    orders.amount
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

Customers without orders are also returned.

## Right Join

Returns all rows from the right table.

```sql
SELECT
    customers.customer_name,
    orders.amount
FROM customers
RIGHT JOIN orders
ON customers.customer_id = orders.customer_id;
```

## Full Join

Returns all rows from both tables.

```sql
SELECT
    customers.customer_name,
    orders.amount
FROM customers
FULL JOIN orders
ON customers.customer_id = orders.customer_id;
```

# Aggregations and Filters

Aggregation functions calculate values from multiple rows.

Common functions are:

* COUNT
* SUM
* AVG
* MIN
* MAX

## COUNT

Counts rows.

```sql
SELECT COUNT(*)
FROM orders;
```

## SUM

Calculates the total.

```sql
SELECT SUM(amount)
FROM orders;
```

## AVG

Calculates the average.

```sql
SELECT AVG(amount)
FROM orders;
```

## GROUP BY

Groups rows before aggregation.

```sql
SELECT
    customer_id,
    SUM(amount)
FROM orders
GROUP BY customer_id;
```

This gives the total order amount for each customer.

## WHERE Filter

Filters rows before grouping.

```sql
SELECT *
FROM orders
WHERE amount > 1000;
```

## HAVING Filter

Filters grouped results.

```sql
SELECT
    customer_id,
    SUM(amount)
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 5000;
```

WHERE filters rows.

HAVING filters groups.

# Normalization

Normalization is the process of organizing database tables to reduce duplicate data and avoid update problems.

The main normal forms are:

* First Normal Form
* Second Normal Form
* Third Normal Form

## First Normal Form

Each column should contain one value.

Bad design:

```text
student_id | subjects
1          | Math, Science
```

Better design:

```text
student_id | subject
1          | Math
1          | Science
```

## Second Normal Form

The table must already be in first normal form.

Every non-key column should depend on the complete primary key.

Suppose the primary key is:

```text
student_id + course_id
```

A column that depends only on student_id should be moved to another table.

## Third Normal Form

The table must already be in second normal form.

Non-key columns should not depend on other non-key columns.

Example:

```text
employee_id
department_id
department_name
```

department_name depends on department_id.

A better design is:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT
);
```

This reduces repeated department names.

# Indexes

Indexes improve the speed of queries.

Without an index, the database may scan every row.

Consider this table.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    email VARCHAR(100)
);
```

Create an index on email.

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

Now this query can be faster.

```sql
SELECT *
FROM employees
WHERE email = 'user@example.com';
```

Indexes are useful for columns that are frequently used in:

* WHERE
* JOIN
* ORDER BY

Indexes also have a cost.

Every INSERT, UPDATE, or DELETE may need to update the index.

Therefore, indexes should be created only where they are useful.

# Transactions

A transaction is a group of SQL statements that are executed together.

The basic commands are:

* BEGIN
* COMMIT
* ROLLBACK

## Example

```sql
BEGIN;

INSERT INTO orders
VALUES (101, 1, 2500);

UPDATE customers
SET total_orders = total_orders + 1
WHERE customer_id = 1;

COMMIT;
```

Both statements become permanent together.

## Rollback Example

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

ROLLBACK;
```

The update is canceled.

Transactions are useful when multiple changes must either all succeed or all fail.

# Locking Mechanism

Locks control how multiple transactions access the same data.

They prevent conflicting changes.

There are two common types.

* Shared lock
* Exclusive lock

## Shared Lock

A shared lock allows reading.

Multiple transactions can read the same row.

```sql
SELECT *
FROM accounts
WHERE account_id = 1;
```

## Exclusive Lock

An exclusive lock is used when modifying data.

```sql
UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;
```

Other transactions may need to wait until the update is finished.

## Row Lock

Locks only the affected row.

```sql
UPDATE employees
SET salary = 50000
WHERE employee_id = 10;
```

## Table Lock

Locks the whole table.

This is less common in modern databases because it reduces concurrency.

Locks help prevent problems such as two users updating the same record at the same time.

# Database Isolation Levels

Isolation levels define how transactions see changes made by other transactions.

The common isolation levels are:

* Read Uncommitted
* Read Committed
* Repeatable Read
* Serializable

## Read Uncommitted

This is the lowest isolation level.

A transaction may read data that has not yet been committed.

Example:

```sql
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

It can produce dirty reads.

## Read Committed

A transaction reads only committed data.

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

This prevents dirty reads.

It is a common default in many databases.

## Repeatable Read

Rows read during a transaction remain unchanged from that transaction's point of view.

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

Reading the same row again returns the same value.

## Serializable

This is the highest isolation level.

Transactions behave as if they run one after another.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

It provides the strongest consistency but may reduce performance because transactions can wait more often.

# Triggers

A trigger is a database object that automatically runs when a specific event happens.

Common events are:

* INSERT
* UPDATE
* DELETE

Triggers are often used for auditing or maintaining related data.

## Example Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Create an audit table.

```sql
CREATE TABLE employee_audit (
    employee_id INT,
    old_salary DECIMAL(10,2),
    new_salary DECIMAL(10,2)
);
```

Create a trigger.

```sql
CREATE TRIGGER salary_change
AFTER UPDATE ON employees
FOR EACH ROW
INSERT INTO employee_audit
VALUES (
    OLD.employee_id,
    OLD.salary,
    NEW.salary
);
```

Now when an employee's salary changes, the trigger automatically stores the old and new salary.

Update an employee.

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;
```

The audit table is automatically updated.

## Another Trigger Example

A trigger can also run after inserting an order.

```sql
CREATE TRIGGER order_created
AFTER INSERT ON orders
FOR EACH ROW
UPDATE customers
SET total_orders = total_orders + 1
WHERE customer_id = NEW.customer_id;
```

Whenever a new order is inserted, the customer's order count is updated automatically.


## Reference

- https://www.postgresql.org/docs/
- https://www.ibm.com/think/topics/cap-theorem
- https://www.postgresql.org/docs/current/sql-createtrigger.html
- https://www.ibm.com/think/topics/relational-databases
