1. Understand the Goal
You need to:

Create at least one stored procedure and one stored function.

Use parameters and conditional logic.

Submit everything to GitHub with a short README.md.

2. Pick Your Database Tool
From your instructions, you can use:

MySQL Workbench (Recommended if you want full procedure/function support)

DB Browser for SQLite (but note: SQLite doesn’t have full stored procedure support—MySQL is better here)

3. Create a Sample Database
Let’s make a simple database for demonstration
create database companydb
use companydb
go

create table employees (emp_id int primary key,emp_name varchar(50),department varchar(50),salary float)

insert into employees values(1,'akhil','HR',30000)
insert into employees values(2,'suri','IT',40000)
insert into employees values(3,'chintu','FINANCE',50000)

select*from employees

DELIMITER //
CREATE PROCEDURE UpdateSalaryByDept(
    IN deptName VARCHAR(50),
    IN percentage DECIMAL(5,2)
)
BEGIN
    UPDATE Employees
    SET Salary = Salary + (Salary * (percentage / 100))
    WHERE Department = deptName;
END //

CALL UpdateSalaryByDept('IT', 10);

DELIMITER //
CREATE FUNCTION GetAnnualSalary(empId INT)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE annualSalary DECIMAL(10,2);
    SELECT Salary * 12 INTO annualSalary
    FROM Employees
    WHERE EmpID = empId;
    RETURN annualSalary;
END //
DELIMITER ;

SELECT GetAnnualSalary(1);

IF Salary < 60000 THEN
    SET Salary = Salary + 5000;
END IF;
