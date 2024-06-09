# Left Join
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

## SQL 1581
```sql
SELECT customer_id,COUNT(customer_id) AS count_no_trans
FROM Visits
LEFT JOIN Transactions ON Visits.visit_id=Transactions.visit_id
WHERE transaction_id is null
GROUP BY customer_id;
```

## SQL 1661
```sql
select a1.machine_id, round(avg(a2.timestamp-a1.timestamp), 3) as processing_time 
from Activity a1
join Activity a2 
on a1.machine_id=a2.machine_id and a1.process_id=a2.process_id
and a1.activity_type='start' and a2.activity_type='end'
group by a1.machine_id;
```
