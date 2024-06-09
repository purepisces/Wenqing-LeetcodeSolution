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
