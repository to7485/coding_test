## 1.
```sql
CREATE TABLESPACE project_data
DATAFILE 'C:/Data/project_data.dbf'
SIZE 20M;
```

## 2.
```sql
ALTER USER HR IDENTIFIED BY hrSecure!456;
```
## 3.
```sql
SELECT tablespace_name 
FROM dba_tablespaces;
```
## 4.
```sql
CREATE TABLE departments_demo (
  department_id   NUMBER(4) PRIMARY KEY,
  department_name VARCHAR2(50),
  location_id     NUMBER(4)
);
```
## 5.
```sql
CREATE VIEW it_sales AS
SELECT employee_id, first_name, job_id
FROM employees
WHERE job_id IN ('IT_PROG', 'SA_REP');
```
## 6.
```sql
ALTER TABLE orders
MODIFY order_date NOT NULL;

ALTER TABLE orders
ADD CONSTRAINT chk_amount_positive CHECK (amount >= 1);
```
## 7.
```sql
SELECT o.order_id, c.customer_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id;
```
## 8.
```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
## 9.
```sql
UPDATE employees
SET salary = salary * 1.15
WHERE department_id = 20
  AND salary < (SELECT AVG(salary) FROM employees);
```
## 10.
```sql
DELETE FROM employees
WHERE resign_flag = 'Y';
```