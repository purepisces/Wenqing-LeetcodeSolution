## Primary Key 

A primary key is a column (or a set of columns) in a database table that uniquely identifies each row in that table. Primary keys must contain unique values and cannot contain NULL values. Each table can have only one primary key, and it ensures that each record in the table is unique and can be referenced distinctly.

## Left Join

```sql
SELECT 
    EmployeeUNI.unique_id,
    Employees.name
FROM 
    Employees
LEFT JOIN 
    EmployeeUNI
ON 
    Employees.id = EmployeeUNI.id;
```
Explanation

- FROM Employees: The table specified after the FROM keyword is considered the left table in a LEFT JOIN.
- LEFT JOIN EmployeeUNI ON Employees.id = EmployeeUNI.id: The LEFT JOIN keyword indicates that we are performing a left join between the Employees table (left table) and the EmployeeUNI table (right table).

### SQL 1581
```sql
SELECT customer_id,COUNT(customer_id) AS count_no_trans
FROM Visits
LEFT JOIN Transactions ON Visits.visit_id=Transactions.visit_id
WHERE transaction_id is null
GROUP BY customer_id;
```
## Join

### SQL 1661
```sql
select a1.machine_id, round(avg(a2.timestamp-a1.timestamp), 3) as processing_time 
from Activity a1
join Activity a2 
on a1.machine_id=a2.machine_id and a1.process_id=a2.process_id
and a1.activity_type='start' and a2.activity_type='end'
group by a1.machine_id;
```

## Cross Join
### SQL 1280
```sql
SELECT
    s.student_id,
    s.student_name,
    su.subject_name,
    COUNT(e.student_id) AS attended_exams
FROM
    Students s
CROSS JOIN
    Subjects su
LEFT JOIN
    Examinations e
ON
    s.student_id = e.student_id AND su.subject_name = e.subject_name
GROUP BY
    s.student_id, s.student_name, su.subject_name
ORDER BY
    s.student_id, su.subject_name;
```

## GROUP BY

The `GROUP BY` clause in SQL is used to group rows that have the same values in specified columns into summary rows, like "find the number of customers in each country." It is often used with aggregate functions (`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`) to perform calculations on each group of rows.

### Example:

Consider the following `Sales` table:

| sale_id | product_name | amount | sale_date |
|---------|--------------|--------|-----------|
| 1       | Laptop       | 1000   | 2024-01-01|
| 2       | Laptop       | 1200   | 2024-01-02|
| 3       | Phone        | 800    | 2024-01-02|
| 4       | Phone        | 850    | 2024-01-03|

If you want to find the total sales amount for each product, you can use the `GROUP BY` clause:

```sql
SELECT product_name, SUM(amount) AS total_sales
FROM Sales
GROUP BY product_name;
```
This would produce:

| product_name | total_sales |
|--------------|-------------|
| Laptop       | 2200        |
| Phone        | 1650        |

Here, `GROUP BY product_name` groups the rows by each unique product name, and `SUM(amount)` calculates the total sales amount for each product.



