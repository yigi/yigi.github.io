### SQL Query to find second highest salary of Employee

```sql
select MAX(Salary) from Employee WHERE Salary NOT IN (select MAX(Salary) from Employee
```

### SQL Query to find Max Salary from each department.

```sql
SELECT DeptID, MAX(Salary) FROM Employee  GROUP BY DeptID. 
```


### Write an SQL Query find number of employees according to gender  whose DOB is between 01/01/1960 to 31/12/1975.

```sql
SELECT COUNT(*), sex from Employees  WHERE  DOB BETWEEN '01/01/1960' AND '31/12/1975'  GROUP BY sex
```


### Write an SQL Query to find name of employee whose name Start with ‘M’

```sql
SELECT * FROM Employees WHERE EmpName like 'M%';
```

