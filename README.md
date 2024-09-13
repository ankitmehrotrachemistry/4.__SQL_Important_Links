# SQL Theory

**1). Primary Key** is one of the candidate keys. One of the candidate keys is selected as the most important and becomes the primary key. There cannot be more than one primary key in a table.  

**2). Foreign key** is a field that can uniquely identify each row in another table. And this constraint is used to specify a field as a Foreign key.

**3). Stored Procedures** Stored Procedure is a function consists of many SQL statement to access the database system. Several SQL statements are consolidated into a stored procedure and execute them whenever and wherever required.

**4.1). BETWEEN:** The BETWEEN operator is used to fetch rows based on a range of values.  
For example,   

```sql
SELECT * FROM Students   
WHERE ROLL_NO BETWEEN 20 AND 30;  
```

**4.2). IN:** The IN operator is used to check for values contained in specific sets.  
For example, 

```sql
SELECT * FROM Students   
WHERE ROLL_NO IN (20,21,23);
```

This query will select all those rows from the table Students where the value of the field ROLL_NO is either 20 or 21 or 23.

**5). JOIN** statement is used to combine data or rows from two or more tables based on a common field between them.

**6.1). Index :** A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and the use of more storage space to maintain the extra copy of data. 

**6.2). Indexing :** Indexing makes columns faster to query by creating pointers to where data is stored within a database.
[Indexing](https://www.atlassian.com/data/sql/how-indexing-works)

**7). Trigger :** is a statement that a system executes automatically when there is any modification to the database. In a trigger, we first specify when the trigger is to be executed and then the action to be performed when the trigger executes. Triggers are stored procedures that automatically execute in response to specific events on a table (like INSERT, UPDATE, DELETE). They can be used for data validation, enforcing business logic, or maintaining data consistency.  

**8). Cluster and Non-Cluster Index :**
| Clustered Index | Non-Clustered Index |
|----------|----------|
| The clustered index is faster.    | The non-clustered index is slower. |
| The clustered index requires less memory for operations.    | The non-Clustered index requires more memory for operations.   | 
| A table can have only one clustered index.    | A table can have multiple non-clustered indexes. |
| In the Clustered index, the Clustered key defines the order of data within the table.    | In the Non-Clustered index, the index key defines the order of data within the index.   | 
| In a clustered index, the index is the main data.    | In the Non-Clustered index, the index is a copy of data. |

[What is the difference between Clustered and Non-Clustered Indexes in SQL Server?](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)

**9). DROP and TRUNCATE statements :**
| DROP | TRUNCATE |
|----------|----------|
| The DROP command is used to remove the table definition and its contents.    | Whereas the TRUNCATE command is used to delete all the rows from the table. |
| In the DROP command, table space is freed from memory.    | While the TRUNCATE command does not free the table space from memory.   | 
| In the DROP command, a view of the table does not exist.    | While in this command, a view of the table exists. |
| The DROP command is quick to perform but gives rise to complications.    | While this command is faster than DROP.   | 

**10). How do we avoid getting duplicate entries in a query without using the distinct keyword?**  
DISTINCT is useful in certain circumstances, but it has drawbacks that it can increase the load on the query engine to perform the sort (since it needs to compare the result set to itself to remove duplicates). We can remove duplicate entries using the following options:
- Remove duplicates using row numbers.
- Remove duplicates using self-Join.
- Remove duplicates using group by.

**11). What is the difference between COALESCE() & ISNULL()?**  
- **COALESCE():** COALESCE function in SQL returns the first non-NULL expression among its arguments. If all the expressions evaluate to null, then the COALESCE function will return null.
Syntax:
```sql
SELECT column(s), CAOLESCE(expression_1,….,expression_n)FROM table_name;
```

- **ISNULL():** The ISNULL function has different uses in SQL Server and MySQL. In SQL Server, ISNULL() function is used to replace NULL values.
Syntax:
```sql
SELECT column(s), ISNULL(column_name, value_to_replace)FROM table_name;
```

**12). How can you optimize a slow-running query?**  
There are several techniques, including:

- Using appropriate indexes
- Avoiding unnecessary joins and subqueries
- Using efficient functions and operators
- Analyzing execution plans to identify bottlenecks

# SQL query

**1.1). SQL query to find the names of employees starting with ‘A’**

```sql
SELECT *  
FROM Employees  
WHERE EmpName like 'A%' ;  
```

**1.2). SQL query to find the names of employees whose name ends with ‘N’**

```sql
SELECT EmpName
FROM Table_name 
WHERE EmpName LIKE '%N' ;  
```

**1.3). SQL query to find the names of employees having ‘M’ in any position**

```sql
SELECT EmpName
FROM Table_name 
WHERE EmpName LIKE '%M%'; 
```

**1.4). SQL query to find the names of employees not having ‘M’ anywhere**

```sql
SELECT EmpName
FROM Table_name 
WHERE EmpName NOT LIKE '%M%'; 
```

**2). SQL query to create an empty table from an existing table**

```sql
Select *
into studentcopy  
from student  
where 1=2
```

**2.2). SQL query to find duplicates in a table**

```sql
SELECT username, email, COUNT(*)
FROM users
GROUP BY username, email
HAVING COUNT(*) > 1
```

**2.3). SQL Query to  update the salary of employees in the employees table.**

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 123;
```

**2.4). SQL Query to sort records in the ‘employees’ table by last_name in ascending order and then by first_name in descending order.**

```sql
SELECT * 
FROM employees
ORDER BY last_name ASC, first_name DESC;
```

**2.5). SQL query to update the prices in a product column by increasing 5% of the prices in each row.**

```sql
UPDATE table_name SET price = price*1.05; 
```

**2.6). SQL query to calculate the average price of products in each category.**

```sql
SELECT 
    category, 
    AVG(price) AS average_price 
FROM 
    table_name 
GROUP BY 
    category;
```

**3). SQL query to fetch common records from two tables**

```sql
Select studentID  
from student  
INTERSECT  
Select StudentID  
from Exam  
```

**4). SQL query to fetch alternate records from a table**

Records can be fetched for both Odd and Even row numbers -  

To display even numbers-  
```sql
Select studentId  
from (Select rowno, studentId from student)  
where mod(rowno,2)=0  
```

To display odd numbers-  
```sql
Select studentId  
from (Select rowno, studentId from student)  
where mod(rowno,2)=1  
```

**5). SQL query to select unique records from a table**

```sql
Select DISTINCT StudentID, StudentName  
from Student
```

**6). SQL Query to Find Duplicate Records in a Table.**

```sql
SELECT 
    emp_name, 
    COUNT(*) AS DuplicateCount 
FROM 
    Employees 
GROUP BY 
    emp_name 
HAVING 
    COUNT(*) > 1;
```

**6). SQL Query to Calculate the Total Number of Orders Placed by each Customer.**

![image](https://github.com/user-attachments/assets/7ce08f12-0b5e-4c48-b413-afe38e41dd2f)

```sql
SELECT cust_ID, 
       COUNT(*) AS TotalOrders 
FROM Orders 
GROUP BY cust_ID;
```

**6). SQL query to  fetch first 5 characters of the string**

There are many ways to fetch first 5 characters of the string -
```sql
Select SUBSTRING(StudentName,1,5)  
as studentname  
from student
```

```sql
Select LEFT(Studentname,5) as studentname from student
```

**7). SQL query to find the top 5 customers with the highest total order amounts**

```sql
SELECT CustomerID, SUM(OrderAmount) AS TotalOrderAmount  
FROM Orders  
GROUP BY CustomerID  
ORDER BY TotalOrderAmount DESC  
LIMIT 5;  
```

**8). SQL query to find the average salary for each department, excluding employees with salaries above a certain threshold.**

```sql
SELECT Department, AVG(Salary) AS AverageSalary
FROM (
  SELECT Department, Salary
  FROM Employees
  WHERE Salary <= (SELECT MAX(Salary) FROM Employees) / 2
) AS Subquery
GROUP BY Department;
```

**9). SQL query to find the difference in days between the order date and the ship date for each order.**

```sql
SELECT OrderID,  
DATEDIFF(day, OrderDate, ShipDate)  
AS DaysDiff  
FROM Orders;

```

**10). SQL Query to pivot data from rows to columns, showing the total sales for each product category by month.**

```sql
SELECT Month,  
       SUM(CASE WHEN ProductCategory = 'Electronics' THEN Sales ELSE 0 END) AS Electronics,  
       SUM(CASE WHEN ProductCategory = 'Clothing' THEN Sales ELSE 0 END) AS Clothing,  
       ... (add more categories)  
FROM SalesData  
GROUP BY Month;  
```

**11). SQL query to find those employees who receive the highest salary of each department. Return employee name and department ID**

![image](https://github.com/user-attachments/assets/787f9ecd-f430-4c1d-b9af-7893f518b1b4)

```sql
SELECT 
    e.emp_name, e.dep_id
FROM 
    employees e
WHERE 
    e.salary = ( SELECT MAX(salary) 
                FROM employees e2 
                WHERE e2.dep_id = e.dep_id );
```


**11.1). SQL Query to find the nth highest salary in an employee table.**

```sql
SELECT Salary  
FROM Employees  
WHERE Salary IN (  
  SELECT TOP 1 Salary  
  FROM (  
    SELECT Salary, ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum  
    FROM Employees  
  ) AS Subquery  
  WHERE RowNum = n  
);  
```

**11.2). SQL Query to get the third-highest salary of an employee from employee_table.**

**Method 1 :**

```sql
SELECT TOP 1 salary
FROM (
  SELECT TOP 3 salary
  FROM employee_table
  ORDER BY salary DESC
) AS emp
ORDER BY salary ASC;
```

**Method 2 :**

```sql
SELECT Max(salary) 
FROM employee 
WHERE salary < (SELECT Max(salary) 
FROM employee 
WHERE salary NOT IN(SELECT Max(salary) 
FROM employee))
```

**11.3). SQL Query to get second highest salary from the following table.**

![image](https://github.com/user-attachments/assets/ab41d077-31d4-4fa0-a84f-563bb96e12d6)

**Method 1**
```sql
SELECT * FROM employee;

SELECT MAX(e_salary) FROM employee
WHERE e_salary NOT IN (SELECT MAX(e_salary)FROM employee);
```

**Method 2**
```sql
SELECT MAX(Salary) AS salary 
FROM Employees 
WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```

**12). SQL Query to  find the total number of customers who placed orders in each quarter of the last year.**

```sql
SELECT DATEPART(quarter, OrderDate) AS Quarter, COUNT(DISTINCT CustomerID) AS Customers  
FROM Orders  
WHERE OrderDate >= DATEADD(year, -1, GETDATE())  
GROUP BY DATEPART(quarter, OrderDate)  
ORDER BY Quarter;  
```

**13). SQL Query to to find the product categories with the highest and lowest total sales for the previous year.**

```sql
SELECT ProductCategory, SUM(SalesAmount) AS TotalSales  
FROM SalesData  
WHERE SaleDate >= DATEADD(year, -1, GETDATE())  
GROUP BY ProductCategory  
ORDER BY TotalSales DESC, TotalSales ASC  
LIMIT 2;  
```

**14). SQL Query to  get the last record from a table.**

```sql
SELECT * 
FROM your_table_name 
ORDER BY your_primary_key_column DESC
LIMIT 1;
```

## JOIN Based Questions

**1). SQL query to find the manager for each employee in a company, even if the employee doesn't have a manager assigned.**

```sql
SELECT e.EmployeeID, m.ManagerName
FROM Employees e
LEFT JOIN Employees m ON e.ManagerID = m.EmployeeID;

```

**2). SQL query to find employees who have never placed an order.**

```sql
SELECT e.EmployeeID, e.EmployeeName  
FROM Employees e  
LEFT JOIN Orders o ON e.EmployeeID = o.CustomerID  
WHERE o.CustomerID IS NULL;

```

**3). SQL query to find the department with the highest average salary for employees who have been with the company for more than 2 years.**

```sql
SELECT d.DepartmentName, AVG(e.Salary) AS AverageSalary  
FROM Employees e  
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID  
WHERE e.HireDate < DATEADD(year, -2, GETDATE())  
GROUP BY d.DepartmentName  
ORDER BY AverageSalary DESC  
LIMIT 1;  

```

**4). SQL query to find the manager hierarchy for a specific employee, showing all levels up to the CEO.**

```sql
WITH ManagerHierarchy (EmployeeID, ManagerID, Level) AS (  
  SELECT EmployeeID, ManagerID, 1 AS Level  
  FROM Employees  
  WHERE EmployeeID = <employee_id>  
  UNION ALL  
  SELECT e.EmployeeID, m.ManagerID, h.Level + 1  
  FROM Employees e  
  INNER JOIN ManagerHierarchy h ON e.EmployeeID = h.ManagerID  
  INNER JOIN Employees m ON e.ManagerID = m.EmployeeID  
  WHERE m.ManagerID IS NOT NULL  
)  
SELECT EmployeeID, ManagerID, Level  
FROM ManagerHierarchy  
ORDER BY Level DESC;  
```

**5). SQL query to find employees who earn more than the average salary in their department.**

```sql
SELECT e.EmployeeID, e.EmployeeName, e.Salary, e.DepartmentID  
FROM Employees e  
JOIN (  
    SELECT DepartmentID, AVG(Salary) AS AvgSalary  
    FROM Employees  
    GROUP BY DepartmentID  
) dept_avg  
ON e.DepartmentID = dept_avg.DepartmentID  
WHERE e.Salary > dept_avg.AvgSalary;  
```

**6). SQL query to Find employees with salary more than their manager's salary.**

```sql
SELECT e.EmployeeID, e.EmployeeName, e.Salary, m.EmployeeName AS ManagerName, m.Salary AS ManagerSalary
FROM Employees e
JOIN Employees m ON e.ManagerID = m.EmployeeID
WHERE e.Salary > m.Salary;
```

## Tricky Interview Question

<p align="center">
  <img src="https://github.com/user-attachments/assets/768befff-5477-4bfe-82c1-64b678edf436" width="400" height="300" />
</p>

**1. Find the total number of orders placed by each customer, excluding orders placed in June.**

```sql
SELECT c.name, COUNT(*) AS num_orders
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id
WHERE MONTH(order_date) <> 6
GROUP BY c.name
```

**2. Find the customer who has placed the highest total order value.**

```sql
SELECT c.name, SUM(order_total) AS total_order_value
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id
GROUP BY c.name
ORDER BY total_order_value DESC
LIMIT 1;
```

**3. List all orders placed on specific dates (eg., 2023-07-04 and 2023-07-06) and their corresponding customer names.**

```sql
SELECT c.name, o.order_date, o.order_total
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id
WHERE order_date IN ('2023-07-04', '2023-07-06');
```

**4. Find the average order value for each city.**

```sql
SELECT c.city, AVG(o.order_total) AS avg_order_value
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id
GROUP BY c.city
```

**5. Identify customers who haven't placed any orders.**

```sql
SELECT c.name
FROM Customers c
LEFT JOIN Orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

**6. Find the month with the highest total order value.**

```sql
SELECT MONTH(order_date) AS order_month, SUM(order_total) AS total_order_value
FROM Orders
GROUP BY MONTH(order_date)
ORDER BY total_order_value DESC
LIMIT 1;
```

**7. Write a query to display the top 2 customers with the most orders in the last 30 days.**

```sql
SELECT c.name, COUNT(*) AS num_orders
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id
WHERE order_date >= DATE_SUB (CURDATE)
```
