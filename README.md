# 1). SQL Theory

## Done upto Pg 14(SQL Problems for Single Table - Level I)    

**1.1). Primary Key** is one of the candidate keys. One of the candidate keys is selected as the most important and becomes the primary key. There cannot be more than one primary key in a table.  
A primary key is a column of a table that uniquely identifies each tuple (row) in that table. Only one primary key is allowed to use in a table.  

**Role of primary Key**
The primary role of a primary key is to enforce the uniqueness of records in a table, ensuring that no two rows have the same primary key value.  
It also facilitates quick data retrieval by providing a straightforward way to look up records. When records are indexed by the primary key, searching and sorting operations become significantly more efficient.  

**1.2). Unique Key** Unique Key constraints also identify an individual tuple uniquely in a relation or table. A table can have more than one unique key, unlike a primary key. Unique Keys can be formed from one or more tables.

<p align="center">
  <img src="https://github.com/user-attachments/assets/aa3648ee-924a-4a76-a1da-27a2e1ce18d1" width="650" height="350" />
</p>

**1.3). Foreign key** is a field that can uniquely identify each row in another table. And this constraint is used to specify a field as a Foreign key.  
A foreign key is a field (or collection of fields) in one table, that references the primary key of another table. The foreign key effectively establishes a link between the records in two tables, maintaining referential integrity within the database.  

**Role of Foreign Key**  
Foreign keys enable the representation of relationships between data by linking records in different tables. This is vital for relational databases where interconnected data is stored across multiple tables.

**Difference between Primary and Foreign Key**  
- The primary key is a unique identifier within its table, whereas a foreign key is a reference in one table to a primary key in another.
- Primary keys enforce uniqueness within their table, ensuring each record is identifiable. Foreign keys, however, are used to establish and navigate relationships between tables.

[Primary Key vs. Foreign Key: Unlocking Efficient Data Management in Databases](https://www.pingcap.com/article/primary-key-vs-foreign-key-unlocking-efficient-data-management-in-databases/#:~:text=The%20primary%20key%20is%20a,and%20navigate%20relationships%20between%20tables.)

**2). CTE (Common Table Expression)**  
A Common Table Expression (CTE) in SQL is a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement. CTEs are defined using the WITH keyword and allow you to create a named, reusable subquery within your SQL statement. They provide a way to simplify complex queries and make them more readable.

**When you would use it ?**

You would use a CTE when you want to:
- **Simplify complex queries:** Break down a complex SQL statement into smaller, more manageable parts to improve readability and maintainability.
- **Avoid duplicating subqueries:** Reuse a result set across multiple parts of a query without rewriting the same subquery multiple times.
- **Create recursive queries:** When you need to perform recursive operations, such as traversing hierarchical data structures.
- **Improve query organization:** Organize your SQL statements by separating logical sections, making it easier to understand and debug.

[SQL Common Table Expression (CTE)](https://hightouch.com/sql-dictionary/sql-common-table-expression-cte)

**3.1). Stored Procedures**  
- Stored Procedure is a function consists of many SQL statement to access the database system. 
- Several SQL statements are consolidated into a stored procedure and execute them whenever and wherever required.
- A SQL Stored Procedure is a named set of one or more SQL statements that can be executed together. 
- It is a database object that is created and stored in the database management system. 
- Stored procedures are typically used for performing common database operations, data processing, and automation of complex tasks. 
- They are particularly valuable for enhancing database security, modularity, and code reusability.

[SQL Stored Procedures](https://hightouch.com/sql-dictionary/sql-stored-procedures)

<p align="center">
  <img src="https://github.com/user-attachments/assets/5b6c82c4-4a5c-4719-becd-bb77213e048e" width="700" height="400" />
</p>

**When you would use it?**   
You would use SQL Stored Procedures when you want to:  
**1. Enhance security:** By allowing controlled access to database operations and reducing the risk of SQL injection attacks.  
**2. Modularize code:** To break down complex SQL logic into manageable, reusable modules for improved maintainability.  
**3. Improve performance:** By reducing the overhead of repeatedly sending SQL statements to the database.  
**4. Automate tasks:** For automating routine or complex database operations and data processing tasks.  
**5. Implement business logic:** To encapsulate business rules and processes directly in the database.  

**3.2). How we can create Stored Procedures?**  
The syntax for creating and executing a SQL Stored Procedure varies slightly depending on the database management system (DBMS) being used. However, here's a generic template:
```sql
CREATE PROCEDURE procedure_name
    (parameter1 data_type, parameter2 data_type, ...)
AS
BEGIN
    -- SQL statements and logic
END;
```

[Learn about Stored Procedures in SQL](https://www.boardinfinity.com/blog/learn-about-stored-procedures-in-sql/)

- procedure_name: The name of the stored procedure.
- (parameter1, parameter2, ...): Optional input parameters for the procedure.
- data_type: The data type for each parameter.
- AS BEGIN ... END: The block of SQL statements and logic to be executed by the procedure.

**Example query**
Here's an example of a simple SQL Stored Procedure in SQL Server that retrieves the names of employees working in a specific department:  
```sql
CREATE PROCEDURE GetEmployeesInDepartment
    @DepartmentID INT
AS
BEGIN
    SELECT EmployeeName
    FROM Employees
    WHERE DepartmentID = @DepartmentID;
END;
```

▶️ [Passing Large Datasets into SQL Server Stored Procedures](https://www.youtube.com/watch?app=desktop&v=jXBYULaUMMs)

**3.3). I have an existing Stored Procedure and it has Performance Issues. What’s the ways I can look upon this issue?** <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**OR**  <br>**How to optimize a Stored Procedure or SQL Query?**  

1. Use SET NOCOUNT ON. [SET NOCOUNT ON statement usage and performance benefits in SQL Server](https://www.sqlshack.com/set-nocount-on-statement-usage-and-performance-benefits-in-sql-server/)    
2. Specify column names instead of using * in SELECT statement.  
3. Use schema name before objects or tablenames.  
Example: SELECT EmplD, Name FROM dbo. Employee  
4. Do not use DYNAMIC QUERIES. They are vulnerable to SQL Injections.  
5. Use EXISTS () instead of COUNT().  
Example :SELECT Count(1) FROM dbo. Employee  
Example: IF( EXISTS (SELECT 1 FROM db Employees))  
6. Use TRANSACTION when required only  

▶️ [SQL Query Optimization | SQL Query Optimization and performance tuning](https://www.youtube.com/watch?v=xYg_aycpp2Q)

**3.4). How to handle Errors in the Stored Procedure ?**
The TRY..CATCH block is used in SQL Server to gracefully handle exceptions. A TRY block may be used to contain a collection of T-SQL queries. When an error occurs in the TRY block, control is then transferred to the CATCH block, which contains further SQL queries to deal with the problem. System methods like ERROR NUMBER(), ERROR STATE(), and ERROR SEVERITY() can be used in the CATCH block to retrieve information about errors. 

The uspEmpUpdate stored procedure error is handled in the example that follows.  

```sql
CREATE PROCEDURE uspUpdateEmpSalary
(
     @empId int
     ,@salary float
)
AS
BEGIN TRY
    UPDATE dbo.Employee
    SET Salary = @salary
    WHERE EmployeeID = @empId
END TRY
BEGIN CATCH
    SELECT
     ERROR_NUMBER() AS ErrorNumber  
     ,ERROR_SEVERITY() AS ErrorSeverity  
     ,ERROR_STATE() AS ErrorState  
     ,ERROR_MESSAGE() AS ErrorMessage;
END CATCH
```

**3.5). What is the difference between Stored Procedure and Functions ?**

| Stored Procedure | Functions |
|----------|----------|
| It is a mini batch program or set of SQL statements.    | Function is also a set of SQL statements and it is used to get computed values or to perform computation. |
| It can change the database environment.    | Function will not make any permanent changes to the database environment. | 
| Select - Insert — update — delete statements are allowed.   | In function, only select statement is allowed, insert — update — delete are not allowed.|
| Stored procedures cannot be executed from select, where or functions.    | It can be called from select, where, or stored procedures.   | 
| Stored procedures can have single or multiple outputs.    | Mostly function returns scalar values / single values. |
| It can return zero or N values.   | Function can return single / scalar value which is compulsory. |
| We can use functions inside the stored procedure.   | Stored procedures cannot be used inside the functions. | 
| Error handling is possible using try catch in stored procedure.   | Error handling is not possible using try catch in functions.|
| Transactions are possible in Stored Procedures.    | Transactions are not possible in functions.   | 
| Stored Procedures can be called using exec / execute keyword followed by the Stored Procedure name.    | Functions can be called by using the select statement followed by the function name. |

▶️ [Functions VS Stored Procedures | SQL Interview Questions And Answers](https://www.youtube.com/watch?v=Qnl95y4IiuU&t=322s)

**One Liner :** 
- Stored procedure is a mini batch program which can do anything, make permanent changes, backup database.
- Function can return computed scalar values. You cannot make permanent changes, means you cannot use insert, update, delete statements inside functions.

**4). Can Functions return Multiple Values in SQL ?**

**5.1). BETWEEN:** The BETWEEN operator is used to fetch rows based on a range of values.  
For example,   

```sql
SELECT * FROM Students   
WHERE ROLL_NO BETWEEN 20 AND 30;  
```

**5.2). IN:** The IN operator is used to check for values contained in specific sets.  
For example, 

```sql
SELECT * FROM Students   
WHERE ROLL_NO IN (20,21,23);
```

This query will select all those rows from the table Students where the value of the field ROLL_NO is either 20 or 21 or 23.

**6). JOIN** statement is used to combine data or rows from two or more tables based on a common field between them. 

**Types of Joins**

![image](https://github.com/user-attachments/assets/da96dbfb-1021-4c83-ba5d-28e5c8247171)

**7.1). Index :** A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and the use of more storage space to maintain the extra copy of data. 

**7.2). Indexing :** Indexing makes columns faster to query by creating pointers to where data is stored within a database.
[Indexing](https://www.atlassian.com/data/sql/how-indexing-works)

**7.3). Cluster and Non-Cluster Index :**

**Clustered Index:**  
- A B-Tree (computed) clustered index is the index that will arrange the rows physically in the memory in sorted order.
- When the Primary Key is created automatically the Clustered Index is created.
- An advantage of a clustered index is that searching for a range of values will be fast.
- A clustered index is internally maintained using a B-Tree data structure leaf node of the b tree of clustered indexes that will contain the table data.
- You can create only one clustered index for a table.

**Syntax :**  
```sql
Create CLUSTERED index IX_Employee_Indexl on Employee_Index(Emp_ID)
```

**Non-Clustered Index:**  
- When a Unique Key is created automatically, a Non-clustered Index is created.
- A non-clustered index is an index that will not arrange the rows physically in the memory in sorted order.
- An advantage of a non-clustered index is searching for the values that are in a range will be fast.
- You can create a maximum of 999 non-clustered indexes on a table, which is 254 up to SQL Berver 2005.
- A non-clustered index is also maintained in a B-Tree data structure but leaf nodes of a B-Tree or non-clustered index contain the pointers to the pages that contain the table data and not the table data directly.

**Syntax :**  
```sql
Create NONCLUSTERED index IX_Employee_NonCIndex on Employee _NonCIndex(Emp_ID)
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/dca0b4ac-abf7-4072-aeb9-2496f2a6bbbe" width="650" height="350" />
</p>

▶️ [19. Clustered Index Vs Non-Clustered Index| Index in SQL by Pandey Guruji in Hindi](https://www.youtube.com/watch?v=BIZTfmuOcm8)

| Clustered Index | Non-Clustered Index |
|----------|----------|
| The clustered index is faster.    | The non-clustered index is slower. |
| The clustered index requires less memory for operations.    | The non-Clustered index requires more memory for operations.   | 
| A table can have only one clustered index.    | A table can have multiple non-clustered indexes. |
| In the Clustered index, the Clustered key defines the order of data within the table.    | In the Non-Clustered index, the index key defines the order of data within the index.   | 
| In a clustered index, the index is the main data.    | In the Non-Clustered index, the index is a copy of data. |

[What is the difference between Clustered and Non-Clustered Indexes in SQL Server?](https://www.sqlshack.com/what-is-the-difference-between-clustered-and-non-clustered-indexes-in-sql-server/)

**8.1). Trigger :**  
- Trigger is a statement that a system executes automatically when there is any modification to the database.
- In a trigger, we first specify when the trigger is to be executed and then the action to be performed when the trigger executes.
- Triggers are piece of logic or set of SQL statements which you want to execute when certain events (insert-update-delete) happens.
- Triggers are stored procedures that automatically execute in response to specific events on a table (like INSERT, UPDATE, DELETE).
- They can be used for data validation, enforcing business logic, or maintaining data consistency.
  
▶️ [Why Do We Need Triggers ? SQL Interview Questions And Answers | SQL Triggers ](https://www.youtube.com/watch?v=lqtKzFKrlfQ&t=251s)

**8.2). How to Create Triggers in SQL?**

▶️ [How to Create Insert Trigger Using SQL Server](https://www.youtube.com/watch?v=KLJ29y3qqyk)

**8.3). Give Example of Custom Triggers in SQL?**

**8.4). Difference between Cursor and Trigger in DBMS :**

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

**12). How can you optimize a slow-running query? / A Query is taking more time to execute. How can we fine tune it?**  
There are several techniques, including:

- Using appropriate indexes
- Avoiding unnecessary joins and subqueries
- Using efficient functions and operators
- Analyzing execution plans to identify bottlenecks

**13). Create Views in Database. Virtual Table in SQL. Why we create SQL View?**  

- In SQL, a view is a virtual table based on the result-set of an SQL statement.
- A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.
- Virtual Tables are not real tables, but can be interacted with as if they were.  

<p align="center">
  <img src="https://github.com/user-attachments/assets/9c5aa065-e16f-4635-9686-211ee564b8d4" width="900" height="550" />
</p>

▶️ [How are virtual tables in SQL used? Virtual Tables in SQL | Nested and complex queries in SQL](https://www.youtube.com/watch?v=NcozPy7TaDw)

**Syntax**
```sql
CREATE VIEW employee_attendance AS 
SELECT first_name, last_name
FROM employees;
```

![image](https://github.com/user-attachments/assets/febf19f0-709f-43aa-8c0d-ed7115a6b5e8)

We will update the Table by adding GMail to them :  
```sql
UPDATE customers
SET email = "PPuff@gmail.com"
WHERE customer_id = 4; // Update all other too in same way
SELECT * FROM customers;
```

![image](https://github.com/user-attachments/assets/734e5430-d62d-42b8-a5bc-7d44e1505524)

```sql
CREATE VIEW customer_emails AS 
SELECT email
FROM customers;
```

- A view is deleted with the DROP VIEW statement.
- The following SQL drops the "Brazil Customers" view:

**Syntax**
```sql
DROP VIEW [Brazil Customers];
```

▶️ [MySQL VIEWS are awesome](https://www.youtube.com/watch?v=wciubfRhvtM)

**14). What are Temporary Tables? What is its Scope? Its types.**

- Temporary tables are tables that exist temporarily on the SQL Server.
- Temporary tables are stored in tempdb.
- They work like a regular table in that you can perform the operations select, insert and delete as for a regular table.
- If created inside a stored procedure they are destroyed upon completion of the stored procedure.

▶️ [Temporary Table in Sql in Hindi | Sql Temporary Table in Hindi](https://www.youtube.com/watch?v=UEJS7hdGqAA)

**How to Create a Temporary SQL Table ?**  
To create a temporary SQL table, we can use the CREATE TABLE statement with the TEMPORARY or TEMP keyword before the table name. Here's an example in SQL:  
```sql
CREATE TEMPORARY TABLE temp_table (
    id INT,
    name VARCHAR(50),
    age INT
);
```

[SQL Temp Table – How to Create a Temporary SQL Table](https://www.freecodecamp.org/news/sql-temp-table-how-to-create-a-temporary-sql-table/)

Temporary SQL tables are a valuable tool in the world of database management and query optimization. They offer various benefits and can significantly enhance your SQL experience.

**15). Window Function in SQL**
Window functions apply ranking and aggregation functions over a certain window (set of rows). The window is defined by the OVER clause when used with window functions. the following two things:
divides rows into groups called sets. (The clause "PARTITION BY" is utilised.)
rows within such partitions are put in a certain sequence. (The clause ORDER BY is utilised.)

<p align="center">
  <img src="https://github.com/user-attachments/assets/e059ca36-96b2-49f7-9449-4b68bc05d314" width="600" height="350" />
</p>

[SQL Window Function](https://www.boardinfinity.com/blog/window-function-in-sql/)

**16). What is the difference between UNION and INTERSECTION ?**
The UNION and INTERSECT operators in SQL allow you to combine the results of two or more SELECT queries and return only unique rows or only rows that are present in both queries, respectively.

<p align="center">
  <img src="https://github.com/user-attachments/assets/454bac7d-5e63-443b-a7de-1c42f2601e33" width="500" height="450" />
</p>

Here is an example of how you can use the UNION operator to combine the results of two SELECT queries:

```sql
SELECT emp_name
FROM Employee
WHERE dept_id = 'D1'

UNION

SELECT dept_name
FROM Department;
```

**Output**

| **emp_name** |  
|Admin|  
| Finance|   
| HR |  
|IT |  
| Manoj|   
| Rahul |  

**17). What is Transaction?**  
A transaction is a set of SQL statements that should be executed as one unit. That means a transaction ensures that either all of the command succeeds or none of them. If one of the commands in the transaction fails, all of the com-
mands fail and any data that is modified in the database is rolled back.

[What is Transaction and Transaction Management in SQL SERVER](https://www.youtube.com/watch?v=ocy9J34liQY)

**How to implement Transaction Management in SQL Server?**  
In order to understand how to implement transaction management in SQL Server, please have a look at the following
list, which shows the Transaction processing steps.
1. Begin Transaction.  
2. Process Database Commands.  
3. Check for Errors ( if occurs RollBack else Commit).  

# 2). SQL query

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

**3). SQL query to find duplicates in a table**

```sql
SELECT username, email, COUNT(*)
FROM users
GROUP BY username, email
HAVING COUNT(*) > 1
```

**4). SQL Query to  update the salary of employees in the employees table.**

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 123;
```

**5). SQL Query to sort records in the ‘employees’ table by last_name in ascending order and then by first_name in descending order.**

```sql
SELECT * 
FROM employees
ORDER BY last_name ASC, first_name DESC;
```

**6). SQL query to update the prices in a product column by increasing 5% of the prices in each row.**

```sql
UPDATE table_name SET price = price*1.05;  
```

**7). SQL query to calculate the average price of products in each category.**

```sql
SELECT 
    category, 
    AVG(price) AS average_price 
FROM 
    table_name 
GROUP BY 
    category;
```

**8). You have an ‘employees’ table and want to classify salaries into categories like "High", "Medium", and "Low". Write SQL Query for the same.**

```sql
SELECT 
    employee_id,
    salary,
    CASE 
        WHEN salary > 70000 THEN 'High'
        WHEN salary BETWEEN 50000 AND 70000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

**9). SQL query to fetch common records from two tables**

```sql
Select studentID  
from student  
INTERSECT  
Select StudentID  
from Exam  
```

**10). SQL Query - If you have two tables, table1 and table2, and you want to find common records based on the same columns.**

```sql
SELECT id, name
 FROM table1
INTERSECT
 SELECT id, name
FROM table2;
```

**11). SQL query to fetch alternate records from a table**

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

**12). SQL query to select unique records from a table**

```sql
Select DISTINCT StudentID, StudentName  
from Student
```

**13). SQL Query to Find Duplicate Records in a Table.**

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

**14). SQL Query to Calculate the Total Number of Orders Placed by each Customer.**

![image](https://github.com/user-attachments/assets/7ce08f12-0b5e-4c48-b413-afe38e41dd2f)

```sql
SELECT cust_ID, 
       COUNT(*) AS TotalOrders 
FROM Orders 
GROUP BY cust_ID;
```

**15). SQL query to  fetch first 5 characters of the string**

There are many ways to fetch first 5 characters of the string -
```sql
Select SUBSTRING(StudentName,1,5)  
as studentname  
from student
```

```sql
Select LEFT(Studentname,5) as studentname from student
```

**16). SQL query to find the top 5 customers with the highest total order amounts**

```sql
SELECT CustomerID, SUM(OrderAmount) AS TotalOrderAmount  
FROM Orders  
GROUP BY CustomerID  
ORDER BY TotalOrderAmount DESC  
LIMIT 5;  
```

**17). SQL query to find the average salary for each department, excluding employees with salaries above a certain threshold.**

```sql
SELECT Department, AVG(Salary) AS AverageSalary
FROM (
  SELECT Department, Salary
  FROM Employees
  WHERE Salary <= (SELECT MAX(Salary) FROM Employees) / 2
) AS Subquery
GROUP BY Department;
```

**18). SQL query to find the difference in days between the order date and the ship date for each order.**

```sql
SELECT OrderID,  
DATEDIFF(day, OrderDate, ShipDate)  
AS DaysDiff  
FROM Orders;

```

**19). SQL Query to pivot data from rows to columns, showing the total sales for each product category by month.**

```sql
SELECT Month,  
       SUM(CASE WHEN ProductCategory = 'Electronics' THEN Sales ELSE 0 END) AS Electronics,  
       SUM(CASE WHEN ProductCategory = 'Clothing' THEN Sales ELSE 0 END) AS Clothing,  
       ... (add more categories)  
FROM SalesData  
GROUP BY Month;  
```

**20.1). SQL query to find those employees who receive the highest salary of each department. Return employee name and department ID**

<p align="center">
  <img src="https://github.com/user-attachments/assets/787f9ecd-f430-4c1d-b9af-7893f518b1b4" width="400" height="250" />
</p>

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


**20.2). SQL Query to find the nth highest salary in an employee table.**

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

**20.3). SQL Query to get the third-highest salary of an employee from employee_table.**

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

**20.4). SQL Query to get second highest salary from the following table.**

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

**21). SQL Query to  find the total number of customers who placed orders in each quarter of the last year.**

```sql
SELECT DATEPART(quarter, OrderDate) AS Quarter, COUNT(DISTINCT CustomerID) AS Customers  
FROM Orders  
WHERE OrderDate >= DATEADD(year, -1, GETDATE())  
GROUP BY DATEPART(quarter, OrderDate)  
ORDER BY Quarter;  
```

**22). SQL Query to to find the product categories with the highest and lowest total sales for the previous year.**

```sql
SELECT ProductCategory, SUM(SalesAmount) AS TotalSales  
FROM SalesData  
WHERE SaleDate >= DATEADD(year, -1, GETDATE())  
GROUP BY ProductCategory  
ORDER BY TotalSales DESC, TotalSales ASC  
LIMIT 2;  
```

**23). SQL Query to  get the last record from a table.**

```sql
SELECT * 
FROM your_table_name 
ORDER BY your_primary_key_column DESC
LIMIT 1;
```

# 3). Comprehensive Question

<p align="center">
  <img src="https://github.com/user-attachments/assets/daf1b7c0-3b06-4c2e-898d-3e5f20461aaa" width="600" height="300" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/baaeb7ef-0fe8-49f1-964a-b0b12ac7d327" width="600" height="300" />
</p>

**1). Write a query to fetch the EmpFname from the EmployeeInfo table in upper case and use the ALIAS name as EmpName.**  
```sql
SELECT UPPER(EmpFname) AS EmpName  
FROM EmployeeInfo;
```

**2). Write a query to fetch the number of employees working in the department ‘HR’.**  
```sql
SELECT COUNT(*)
FROM EmployeeInfo
WHERE Department = 'HR';
```

**3). Write a query to get the current date.**  
```sql
SELECT GETDATE();
```

**4). Write a query to retrieve the first four characters of  EmpLname from the EmployeeInfo table.**  
```sql
SELECT SUBSTRING(EmpLname, 1, 4)
FROM EmployeeInfo;
```

**5). Write a query to fetch only the place name(string before brackets) from the Address column of EmployeeInfo table.**  
```sql
SELECT SUBSTRING(Address, 1, CHARINDEX('(',Address))
FROM EmployeeInfo;
```

**6). Write a query to create a new table which consists of data and structure copied from the other table.**  
Using the SELECT INTO command:  
```sql
SELECT * INTO NewTable
FROM EmployeeInfo
WHERE 1 = 0;
```
Using the CREATE command in MySQL:
```sql
CREATE TABLE NewTable AS
SELECT *
FROM EmployeeInfo;
```

**7).  Write q query to find all the employees whose salary is between 50000 to 100000.**  
```sql
SELECT * FROM EmployeePosition
WHERE Salary BETWEEN '50000' AND '100000';
```

**8). Write a query to find the names of employees that begin with ‘S’**  
```sql
SELECT * FROM EmployeeInfo
WHERE EmpFname LIKE 'S%';
```

**9). Write a query to fetch top N records.**  
By using the LIMIT command in MySQL:
```sql
SELECT * FROM EmpPosition
ORDER BY Salary DESC LIMIT N;
```

**10). Write a query to retrieve the EmpFname and EmpLname in a single column as “FullName”. The first name and the last name must be separated with space.**  
```sql
SELECT CONCAT(EmpFname, ' ', EmpLname) AS 'FullName' FROM EmployeeInfo;
```

**11). Write a query find number of employees whose DOB is between 02/05/1970 to 31/12/1975 and are grouped according to gender**  
```sql
SELECT COUNT(*), Gender
FROM EmployeeInfo
WHERE DOB BETWEEN '02/05/1970 ' AND '31/12/1975'
GROUP BY Gender;
```

**12). Write a query to fetch all the records from the EmployeeInfo table ordered by EmpLname in descending order and Department in the ascending order.**  
```sql
SELECT * FROM EmployeeInfo
ORDER BY EmpFname desc, Department asc;
```

**13). Write a query to fetch details of employees whose EmpLname ends with an alphabet ‘A’ and contains five alphabets.**  
```sql
SELECT * FROM EmployeeInfo
WHERE EmpLname LIKE '____a';
```

**14). Write a query to fetch details of all employees excluding the employees with first names, “Sanjay” and “Sonia” from the EmployeeInfo table.**  
```sql
SELECT * FROM EmployeeInfo
WHERE EmpFname
NOT IN ('Sanjay','Sonia');
```

**15). Write a query to fetch details of employees with the address as “DELHI(DEL)”.**  
```sql
SELECT * FROM EmployeeInfo
WHERE Address
LIKE 'DELHI(DEL)%';
```

**16). Write a query to fetch all employees who also hold the managerial position. (JOIN Question)**  
```sql
SELECT E.EmpFname, E.EmpLname, P.EmpPosition 
FROM EmployeeInfo E
INNER JOIN
EmployeePosition P ON
E.EmpID = P.EmpID AND P.EmpPosition IN ('Manager');
```

**17). Write a query to fetch the department-wise count of employees sorted by department’s count in ascending order.**  
```sql
SELECT Department, count(EmpID) AS EmpDeptCount 
FROM EmployeeInfo GROUP BY Department 
ORDER BY EmpDeptCount ASC;
```

**18). Write a query to calculate the even and odd records from a table.**  

To retrieve the even records from a table, you have to use the MOD() function as follows:
```sql
SELECT EmpID
FROM (SELECT rowno, EmpID from EmployeeInfo)
WHERE MOD(rowno,2)=0;
```

Similarly, to retrieve the odd records from a table, you can write a query as follows:
```sql
SELECT EmpID
FROM (SELECT rowno, EmpID from EmployeeInfo)
WHERE MOD(rowno,2)=1;
```

**19). Write a SQL query to retrieve employee details from EmployeeInfo table who have a date of joining in the EmployeePosition table. (Two Table Question)**  
```sql
SELECT * FROM EmployeeInfo E 
WHERE EXISTS 
(SELECT * FROM EmployeePosition P WHERE E.EmpId = P.EmpId);
```

**20). Write a query to retrieve two minimum and maximum salaries from the EmployeePosition table. (Two Table Question)**  

To retrieve two minimum salaries, you can write a query as below:  
```sql
SELECT DISTINCT Salary FROM EmployeePosition E1 
 WHERE 2 >= (SELECTCOUNT(DISTINCT Salary)FROM EmployeePosition E2 
  WHERE E1.Salary >= E2.Salary) ORDER BY E1.Salary DESC;
```

To retrieve two maximum salaries, you can write a query as below:  
```sql
SELECT DISTINCT Salary
FROM EmployeePosition E1 
WHERE 2 >= (SELECTCOUNT(DISTINCT Salary)
FROM EmployeePosition E2 
WHERE E1.Salary <= E2.Salary)
ORDER BY E1.Salary DESC;
```

**21). Write a query to find the Nth highest salary from the table without using TOP/limit keyword.**  
```sql
SELECT Salary 
FROM EmployeePosition E1 
WHERE N-1 = ( 
      SELECT COUNT( DISTINCT ( E2.Salary ) ) 
      FROM EmployeePosition E2 
      WHERE E2.Salary >  E1.Salary );
```

**22). Write a query to retrieve duplicate records from a table.**  
```sql
SELECT EmpID, EmpFname, Department COUNT(*) 
FROM EmployeeInfo GROUP BY EmpID, EmpFname, Department 
HAVING COUNT(*) > 1;
```

**23). Write a query to retrieve the list of employees working in the same department.**  
```sql
Select DISTINCT E.EmpID, E.EmpFname, E.Department 
FROM EmployeeInfo E, Employee E1 
WHERE E.Department = E1.Department AND E.EmpID != E1.EmpID;
```

**24). Write a query to retrieve the last 3 records from the EmployeeInfo table.**  
```sql
SELECT * FROM EmployeeInfo WHERE
EmpID <=3 UNION SELECT * FROM
(SELECT * FROM EmployeeInfo E ORDER BY E.EmpID DESC) 
AS E1 WHERE E1.EmpID <=3;
```

**25).  Write a query to find the third-highest salary from the EmpPosition table.**  
```sql
SELECT TOP 1 salary
FROM(
SELECT TOP 3 salary
FROM employee_table
ORDER BY salary DESC) AS emp
ORDER BY salary ASC;
```

**26). Write a query to display the first and the last record from the EmployeeInfo table.**  

To display the first record from the EmployeeInfo table, you can write a query as follows:
```sql
SELECT *
FROM EmployeeInfo
WHERE EmpID = (SELECT MIN(EmpID) FROM EmployeeInfo);
```

To display the last record from the EmployeeInfo table, you can write a query as follows:
```sql
SELECT * FROM EmployeeInfo
WHERE EmpID = (SELECT MAX(EmpID) FROM EmployeeInfo);
```

**27). Write a query to add email validation to your database.**  
```sql
SELECT Email
FROM EmployeeInfo
WHERE NOT REGEXP_LIKE(Email, ‘[A-Z0-9._%+-]+@[A-Z0-9.-]+.[A-Z]{2,4}’, ‘i’);
```

**28). Write a query to retrieve Departments who have less than 2 employees working in it.**  
```sql
SELECT DEPARTMENT, COUNT(EmpID) as 'EmpNo'
FROM EmployeeInfo
GROUP BY DEPARTMENT
HAVING COUNT(EmpD) < 2;
```

**29). Write a query to retrieve EmpPostion along with total salaries paid for each of them.**  
```sql
SELECT EmpPosition, SUM(Salary)
from EmployeePosition
GROUP BY EmpPosition;
```

**30). Write a query to fetch 50% records from the EmployeeInfo table.**  
```sql
SELECT * FROM EmployeeInfo
WHERE EmpID <= (SELECT COUNT(EmpID)/2 from EmployeeInfo);
```

**31).  How do you read the last five records from a database using a SQL query?**  
```sql
SELECT * 
FROM your_table
ORDER BY id DESC
LIMIT 5;
```

**32). Write a SQL query that will provide you with the 10th-highest employee salary from an Employee table.**  
```sql
SELECT salary
FROM (
    SELECT salary, ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
    FROM Employee
) AS ranked_salary
WHERE row_num = 10;
```

**33). Write a query to get the last record from a table.**  
```sql
SELECT * FROM your_table_name
ORDER BY your_primary_key_column
DESC LIMIT 1;
```

# 4). JOIN Based Questions

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

# 5). Tricky Interview Question

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

# 6). SQL in Game Development

It is used to store player and world related data in a multiplayer games, like MMO games.  
If you're working on a SQL database for a game, especially as a backend developer, you'll likely need to design tables for players, game sessions, leaderboards, inventory, and other relevant features. Here's a basic outline of what a SQL database for a game might look like:

**1. Players Table**
This stores player data such as username, email, password (hashed), and other details.
```sql
CREATE TABLE Players (
    PlayerID INT PRIMARY KEY AUTO_INCREMENT,
    Username VARCHAR(50) NOT NULL,
    Email VARCHAR(100) NOT NULL,
    PasswordHash VARCHAR(255) NOT NULL,
    CreatedAt DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

**2. GameSessions Table**
This stores data about game sessions, such as when they started and ended, and the score the player achieved.
```sql
CREATE TABLE GameSessions (
    SessionID INT PRIMARY KEY AUTO_INCREMENT,
    PlayerID INT,
    StartTime DATETIME,
    EndTime DATETIME,
    Score INT,
    FOREIGN KEY (PlayerID) REFERENCES Players(PlayerID)
);

```

**3. Inventory Table**
This stores data about items players can own within the game.
```csharp
CREATE TABLE Inventory (
    InventoryID INT PRIMARY KEY AUTO_INCREMENT,
    PlayerID INT,
    ItemName VARCHAR(100),
    Quantity INT,
    FOREIGN KEY (PlayerID) REFERENCES Players(PlayerID)
);
```

**4. Leaderboards Table**
This stores leaderboard data, which may be updated periodically based on game results.
```csharp
CREATE TABLE Leaderboards (
    LeaderboardID INT PRIMARY KEY AUTO_INCREMENT,
    PlayerID INT,
    TotalScore INT,
    Rank INT,
    FOREIGN KEY (PlayerID) REFERENCES Players(PlayerID)
);
```

**5. Achievements Table**
This table holds data about achievements or badges players can earn in the game.
```csharp
CREATE TABLE Achievements (
    AchievementID INT PRIMARY KEY AUTO_INCREMENT,
    PlayerID INT,
    AchievementName VARCHAR(100),
    DateUnlocked DATETIME,
    FOREIGN KEY (PlayerID) REFERENCES Players(PlayerID)
);
```

**6. Friends Table**
If your game has a social aspect, you can allow players to add friends.
```csharp
CREATE TABLE Friends (
    PlayerID1 INT,
    PlayerID2 INT,
    FOREIGN KEY (PlayerID1) REFERENCES Players(PlayerID),
    FOREIGN KEY (PlayerID2) REFERENCES Players(PlayerID),
    PRIMARY KEY (PlayerID1, PlayerID2)
);
```
This database design can be expanded based on the specific features of your game, such as guilds, real-time chat, and more complex items or gameplay mechanics.   

**Game Databases**  [Game Databases](https://aws.amazon.com/gametech/databases/)  
Whether it’s leaderboards, virtual goods, or even cheat detection, players generate a ton of data that needs to be processed, stored, and accessed in real-time. Modernize your data infrastructure with AWS fully managed, purpose-built databases to delight your players.  

![image](https://github.com/user-attachments/assets/63cecf73-9b99-4777-a628-3751322698fb)

**Amazon DynamoDB** : Deliver games with consistent single-digit millisecond performnance, nearly unlimited throughput and storage, and automatic multi-region replication.  
Using DynamoDB to store player game state and other player data allows game companies to accommodate high numbers of concurrent players while maintaining millisecond access latency. As an example, consider Electronic Arts (EA), a large video game company with more than 300 million registered players around the world. For EA, high concurrency can mean more than 100,000 requests per second and millions of daily active users. By migrating to DynamoDB, EA realized a 90 percent cost reduction over the old database, a MySQL cluster. EA uses DynamoDB to store game state, user data, and game inventory data in multiple tables. EA uses the user ID as the partition key and primary key (a 1:1 modeling pattern).  
  
**You can refer to Amazon DynamoDB here :** [Amazon DynamoDB](https://aws.amazon.com/blogs/database/amazon-dynamodb-gaming-use-cases-and-design-patterns/)  
- **Use case: Player session history data store**  
Game makers store session history and other time-oriented data in DynamoDB for fast lookup by player, date, and time. For example, Riot Games, which serves international players who create terabytes of data daily, stores player session history in DynamoDB. This allows its Player Support team to look up all the information for a given player quickly, such as all the player’s in-game purchases and last login time.  

- **Use case: Leaderboard** -  
Game makers can support simple leaderboards easily by using DynamoDB. One such use case is the ability to display top scores for a game. If a gaming company already stores players’ game state in DynamoDB, including players’ top scores, the ability to get top scores can be implemented by using a global secondary index.

**Useful Links :**  

[How to Design a Database for Multiplayer Online Games](https://www.geeksforgeeks.org/how-to-design-a-database-for-multiplayer-online-games/)

[Sample Database: Video Games (ERD and SQL)](https://www.databasestar.com/sample-database-video-games/)

[Do Video Games Use Databases?](https://www.dragonflydb.io/faq/do-video-games-use-databases)

[Should I Use Redis or MySQL for Game Development?](https://www.dragonflydb.io/faq/redis-vs-mysql-for-game-development)

[Can I Use an SQL Database for Game Development?](https://www.dragonflydb.io/faq/use-sql-database-game-development)

[Creating account/login system and SQL Database best practices?](https://www.reddit.com/r/unrealengine/comments/fby4xn/creating_accountlogin_system_and_sql_database/)
