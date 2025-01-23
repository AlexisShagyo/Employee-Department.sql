# 🕵️‍♀️Employee Database Management
<img src="https://github.com/AlexisShagyo/fuzzy-octo-computing-machine/blob/main/employee-benefit-expenses.jpg" alt="Image" width="500" height="250">

## Task Overview 📃

Your company doesn't have a database with all the employee information yet. Create one according to the following criteria:
| employee_id | first_name | last_name | job_position| salary | start_date | brith_date | store_id | deprtment_id | manager_id | 
| ----------- | ---------- | --------- | ----------- | ------ | ---------- | -------- | ------------ | ---------- | ------ |

Set up an additional table called departments in the following way:
| department_id | department | division | 
| ------------- | ---------- | -------- |
---

#### _Task 1: Create Tables_

> #### Employee Table:
```sql
CREATE TABLE employee (
    employee_id INT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    job_position VARCHAR(50) NOT NULL,
    salary NUMERIC(8,2),
    start_date DATE NOT NULL,
    birth_date DATE,
    store_id INT,
    department_id INT,
    manager_id INT );
```
> #### Department Table:
```sql
CREATE TABLE department (
    department_id INT NOT NULL,
    department CHAR(50),
    division CHAR(50));
```
-----
#### _Task 2: Delete the birth_date column from employee table as it won't be needed_
> #### Employee Table: 
```sql
Alter Table employee
Drop Column birth_date
```
`Result:`
| employee_id | first_name | last_name | job_position| salary | start_date | store_id | deprtment_id | manager_id | 
| ----------- | ---------- | --------- | ----------- | ------ | ---------- | ------------ | -------- | ---------- |
-----

#### _Task 3: Adding values to the employee and depatment table_
> #### Employee Table:
```sql
Insert into employee VALUES
( 1,'Morrie','Conaboy','CTO',21268.94,'2005-04-30',1,1,6),
(2,'Miller','McQuarter','Head of BI',14614.00,'2019-07-23',1,1,1),
(3,'Christalle','McKenny','Head of Sales',12586.00,'1999-02-05',2,3,1),
(4,'Summer','Siares','SQL Analyst',9515.00,'2006-05-31',2,1,6),
(5,'Romain','Hacard','BI Consultant',7107.00,'2012-09-24',1,1,6),
(6,'Ely','Luscombe','Team Lead Analytics',12564.00,'2002-06-12',1,1,2),
(7,'Clywd','Filyashin','Senior SQL Analyst',10510.00,'2010-04-05',2,1,2),
(8,'Chris','Blague','SQL Analyst',9428.00,'2007-09-30',2,2,6),
(9,'Roddie','Izen','Software Engineer',4937.00,'2019-03-22',1,4,6),
(10,'Ammamaria','Izhak','Customer Support',2355.00,'2005-03-17',2,5,3),
(11,'Carlyn','Stripp','Customer Support',3060.00,'2013-09-06',1,5,3),
(12,'Reuben','McRorie','Software Engineer',7119.00,'1995-12-31',1,5,6),
(13,'Gates','Raison','Marketing Specialist',3910.00,'2013-07-18',1,3,3),
(14,'Jordanna','Raitt','Marketing Specialist',5844.00,'2011-10-23',2,3,3),
(15,'Guendolen','Motton','BI Consultant',8330.00,'2011-01-10',2,3,6),
(16,'Doria','Turbat','Senior SQL Analyst',9278.00,'2010-08-15',1,1,6),
(17,'Cort','Bewlie','Project Manager',5463.00,'2013-05-26',1,5,3),
(18,'Margarita','Eaden','SQL Analyst',5977.00,'2014-09-24',2,1,6),
(19,'Hetty','Kingaby','SQL Analyst',7541.00,'2009-08-17',1,2,6),
(20,'Lief','Robardley','SQL Analyst',8981.00,'2002-10-23',2,3,6),
(21,'Zaneta','Carlozzi','Working Student',1525.00,'2006-08-29',1,3,6),
(22,'Giana','Matz','Working Student',1036.00,'2016-03-18',1,3,6),
(23,'Hamil','Evershed','Web Developper',3088.00,'2022-02-03',1,4,2),
(24,'Lowe','Diamant','Web Developper',6418.00,'2018-12-31',1,4,2),
(25,'Jack','Franklin','SQL Analyst',6771.00,'2013-05-18',1,2,2),
(26,'Jessica','Brown','SQL Analyst',8566.00,'2003-10-23',1,1,2);
```

> #### Department Table:
```sql
Insert Into department VALUES
(1,'Analytics','IT'),
(2,'Finance','Administration'),
(3,'Sales','Sales'),
(4,'Website','IT'),
(5,'Back Office','Administration');
```
`Result:`
| department_id | department | division | 
| ------------- | ---------- | -------- |
|             1 | Analytics  | IT       | 
|             2 | Finance    | Administration | 
|             3 | Sales      | Sales    | 
|             4 | Website    | IT       | 
|             5 | Back Office | Administration | 
-----

#### _Task 3: Jack Franklin gets promoted to 'Senior SQL Analyst' and the salary raises to 7200_
```sql
Update employee 
SET job_position = 'Senior SQL Analyst'
WHERE first_name = 'Jack' AND last_name = 'Franklin';
```
Updating the salary:
```sql
Update employee
SET salary = 7200.00
WHERE first_name = 'Jack' AND last_name = 'Franklin';
```
-----

#### _Task 4: The responsible people decided to rename the job_position Customer Support to Customer Specialist_
```sql
Update employee
SET job_position = 'Customer Specialist'
WHERE job_position = 'Customer Support';
```
-----

#### _Task 5: All SQL Analysts including Senior SQL Analysts get a raise of 6%_
```sql
UPDATE employee
SET salary=salary*1.06
WHERE job_position LIKE '%SQL Analyst';
```
-----

#### _Task 6: What is the average salary of a SQL Analyst in the company (excluding Senior SQL Analyst)?_
```sql
Select ROUND(AVG(salary),2) 
From employee
WHERE job_position = 'SQL Analyst';
```
`Result:`
| 8834.75 | 
| ------- | 
-----

#### _Task 7: What is the average salaries per division?_
```sql
SELECT 
division,
ROUND(AVG(e.salary),2)
FROM employee AS e
LEFT JOIN department AS d 
ON e.department_id=d.department_id
GROUP BY division
ORDER BY 2 ;
```
`Result:`
| division | round |
| ------- | ------ | 
| Sales | 6107.27 |
| Administration | 6230.88 |
| IT | 9706.14 |
-----

#### _Task 8: Select the following: employee_id, first_name, last_name, job_position, salary and return the average salary for every job_position. Round up the average to 2 decimals and order them by employee_id_
```sql
Select employee_id, 
first_name, 
last_name, 
job_position, 
salary, 
ROUND(AVG(salary) OVER(PARTITION BY job_position),2) 
AS ave_salary_position
From employee
Order by employee_id;
```
`Result:`
| employee_id | first_name | last_name | job_position | salary | ave_salary_position | 
| ----------- | ---------- | --------- | ------------ | ------ | ------------------- |
|           1 | Morrie     | Canoboy   |  CTO         | 21268.94 | 21268.94 | 
|           2 | Miller     | McQuarter |  Head of BI  | 14614.00 | 14614.00 | 
|           3 | Christalle | McKenny   | Head of Sales | 12587.00 | 12587.00 | 
|           4 | Summer     | Seares    |  SQL Analyst | 10085.90 | 8834.75 | 
-----

#### _Task 9: How many people are earning less than the Average Salary per Job Position?_
```sql
Select COUNT(*) From ( 
Select salary, ROUND(AVG(salary) 
OVER(PARTITION BY job_position),2) 
AS ave_salary_position
From employee)
Where salary < ave_salary_position ;
```
`Result:`
| 9 | 
| - |
