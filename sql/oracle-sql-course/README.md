# 📊 Oracle SQL Course: SQL Made Practical

<br/>
<br/>
<p align="center"><em> Completed on Aug, 2022 - 223/223 topics</em></strong></p>
<p align="center"><strong>All queries here were written by me on the tasks given by the teacher.</strong></p>

<br/>

## Introduction
<br/>

Click [HERE](https://www.udemy.com/course/oracle-sql-from-scratch/) to take a look at the course.

<br/>

<details> 
<summary>
Click here for Introduction! 👋🏻
	
</summary>
	
<br/>
	
**📈 BIREFING**

- This course aims to teach SQL in a pratical way. Every topic is teached on video and after that, the couse gives a challenge that I had to do it by myself. Thats why some of the queries are a little off topic. It was me exploring learning possibilities within the lesson.

**✏️ OBJECTIVE**

- Be able to use Oracle SQL to retrieve, filter, analyze, format and present information from Oracle databases.
- Understand Oracle SQL code written by other people and feel confident to modify it.
- Be able to use SQL to insert, modify and delete information from Oracle databases.
- Be able to write the SQL code needed to solve the most common problems found in real work situations and academic tests.


**📈 ENVIROMENT SETUP**

- [Oracle LIVE SQL](https://livesql.oracle.com/)

</details> 
<br/>

***

## Table of Contents

- [Retrieving Information](#retrieving-information)
	- [Schema #1](#retrieving-information)
- [Filtering and Sorting](#filtering-and-sorting)
	- [Schema #2](#filtering-and-sorting)
- [Operators](#operators)
- [Group Operations](#group-operations)
 	- [Schema #3](#schema-3)
- [Subqueries in SQL](#subqueries-in-sql)
- [Single Row Functions](#single-row-functions)
- [Transposing](#transposing)
- [Analytic Functions](#analytic-functions)
- [Set Operators](#set-operators)
- [Selecting data from multiple tables](#selecting-data-from-multiple-tables)
	- [More Complex Schema](#more-complex-schema) 
- [Hierarchical Queries](#hierarchical-queries)
- [Additional Practice](#additional-practice)


<br/>
<br/>


## Retrieving Information

<br/>

<details> 
<summary>
Click here this section! I've decided to hide this because its very introductory.
	
</summary>
	
<br/>

**Content**

- [Schema #1](#schema-1)
- [Basic SELECT statement](#basic-select-statement)

<br/>

## Schema #1

<details>
<summary>
Click here to see the script for the tables!
</summary>

```sql
CREATE TABLE department
(
  id	   		number(5) constraint pk_department primary key,
  name	   		varchar2(50),
  monthly_budget 	number(8,2),
  last_employee_id 	number(5)
);

CREATE TABLE employee
(
  id        number(5) constraint pk_employee primary key,
  name      varchar2(50),
  birthdate date,
  phone     varchar2(20),
  salary    number(7,2) not null,
  department_id number(3) constraint fk_employee_department references department,
  hire_date date,
  job_id    varchar2(20),
  email     varchar2(50)
 );


 insert into department values (1,'ACCOUNTING',20000,8);
 insert into department values (2,'MARKETING',15000,9);
 insert into department values (3,'INFORMATION TECHNOLOGY',30000,10);
 insert into department values (4,'HUMAN RESOURCES',25000,13);
 insert into department values (5,'REGULATORY AFFAIRS',5000,null);
 insert into department values (6,'CUSTOMER SERVICE',2000,null);

 insert into employee values (1,'JOHN SMITH',date '1995-01-01','1.123.456.7890',4000.00,1,date '2015-03-28','AC_ACCOUNT','JSMITH');
 insert into employee values (2,'JAMES BOSH',date '1992-02-15','1.234.567.8901',3500.00,2,date '2014-07-01','MK_REP','JBOSH');
 insert into employee values (3,'LUISA JACKSON',date '1970-03-08','1.345.678.9012',4500.00,3,date '2013-08-29','IT_PROG','LJACKSON');
 insert into employee values (4,'STUART GARCIA',date '1965-04-12','1.456.789.0123',2000.00,4,date '2010-02-15','HR_REP','SGARCIA');
 insert into employee values (5,'JUSTIN BLACK',date '1990-05-16','1.567.890.1234',2550.00,1,date '2015-05-02','AC_ACCOUNT','JBLACK');
 insert into employee values (6,'ANGIE CROOD',date '1998-06-22','1.678.901.2345',1500.00,1,date '2015-07-01','AC_ACCOUNT','ACROOD');
 insert into employee values (7,'CHARLES DEAN',date '1973-06-08','1.789.012.3456',2250.00,3,date '2002-03-01','IT_PROG','CDEAN');
 insert into employee values (8,'EDDIE FARREL',date '1980-07-28','1.890.123.4567',3000.00,1,date '2009-04-20','AC_ACCOUNT','EFARREL');
 insert into employee values (9,'GEORGE HAYES',date '1982-08-03',NULL,2500.00,2,date '2012-09-22','MK_REP','GHAYES');
 insert into employee values (10,'IGOR KEYS OSBOURNE',date '1987-09-11','144.898.7564',6000.00,3,date '2014-11-14','IT_PROG','IKEYS');
 insert into employee values (11,'LUKE MINT',date '1985-10-19','1.123.456.7890',5000.00,4,date '2011-01-08','HR_REP','LMINT');
 insert into employee values (12,'NIGEL OAKS',date '1997-11-05','52.987.654.3210',4750.00,4,date '2014-10-01','HR_REP','NOAKS');
 insert into employee values (13,'LUKE GREEN JR',date '1995-02-05',NULL,4750.00,4,date '2015-09-01','HR_REP','LGREEN');
 
CREATE TABLE products
  (
	Product_Id   NUMBER(5),
	Product_Name VARCHAR2(100),
	Price           NUMBER(8,2),
	Expiration_Date DATE
  ) ;
 
ALTER TABLE products ADD CONSTRAINT products_PK PRIMARY KEY ( Product_Id ) ;
 
insert into products values (1,'Aspirin',5,date '2025-12-31');
insert into products values (2,'Penicillin',10,date '2026-04-30');
insert into products values (3,'Insulin',25,date '2026-05-31');
insert into products values (4,'Acetaminophen',5,date '2027-01-31');
insert into products values (5,'Amoxicillin',8,date '2026-07-31');

commit;
```
</details>

<img width="761" alt="Screen Shot 2022-07-18 at 22 54 05" src="https://user-images.githubusercontent.com/59098085/179647475-4f90450a-c2eb-47f6-ac28-5fe7553ed307.png">
	
<img width="443" alt="Screen Shot 2022-07-18 at 22 54 14" src="https://user-images.githubusercontent.com/59098085/179647724-ba10605d-1ea1-43e4-ab37-99d4ef97f48a.png">

<img width="367" alt="Screen Shot 2022-07-25 at 18 19 30" src="https://user-images.githubusercontent.com/59098085/180875905-bd0adc6e-22e1-4f29-a1f7-5a6dec49b1a6.png">

<br/>
	

### Basic SELECT statement


#### 📌 C1: Get the list of names, phones, and salaries of all employees.

```sql
select
    name,
    phone,
    salary
from employee;
```

#### 📌 C2: Retrieve all of the information available in the department table.

```sql
select *
from department;
```

#### 📌 C3: The company is going to give all employees a 20% increase in their salaries, and your task is to display a list of all of the employees which includes the employee id, the name, the current salary, and the salary they will have after the 20% increase.

```sql
select
    id,
    name,
    salary,
    salary*1.2 as raise
from employee;
```
	
</details> 
<br/>

***


## Filtering and Sorting


<br/>

**Content**

- Filtering
	- Schema #2
- [Understanding and Handling NULLs](#understanding-and-handling-nulls)
- [NULL Handling Functions](#null-handling-functions)

<br/>
<br/>

<details> 
<summary>
Click here this section! I've decided to hide this because its very introductory.
	
</summary>

<br/>

### Filtering

<br/>

#### 📌 C4: Display a list of departments whose monthly budget is greater than or equal to 20,000. Please include only the department name and its budget.

```sql
select name,monthly_budget
from department
where monthly_budget >= 20000;
```

#### 📌 C5: Display a list of employees who were born before 1990, which includes the name, phone, and birthdate.

```sql
select Name, phone, birthdate
from employee
where birthdate < date '1990-01-01';
```


#### 📌 C6: The company is planning to give some employees a special gift, but they will consider only employees that work in the accounting and marketing departments.  For employees of those departments, the condition is that they must earn less than 3000 a month, or have been born before the year 1985.  Your task consists of displaying the list of employees that can participate.

Hint: List the contents of the department table to see the IDs you have to use in your condition to return only the marketing and accounting departments.

```sql
select *
from employee
where department_id = 1 or department_id = 2 and salary < 3000 or birthdate < date '1995-01-01';
```

## Schema #2

<details>
<summary>
Click here to see the script for the tables!
</summary>

```sql
CREATE TABLE department
(
  id	   		number(5) constraint pk_department primary key,
  name	   		varchar2(50),
  monthly_budget 	number(8,2),
  last_employee_id 	number(5)
);

CREATE TABLE employee
(
  id        number(5) constraint pk_employee primary key,
  name      varchar2(50),
  birthdate date,
  phone     varchar2(20),
  salary    number(7,2) not null,
  department_id number(3) constraint fk_employee_department references department,
  hire_date date,
  job_id    varchar2(20),
  email     varchar2(50)
 );


 insert into department values (1,'ACCOUNTING',20000,8);
 insert into department values (2,'MARKETING',15000,9);
 insert into department values (3,'INFORMATION TECHNOLOGY',30000,10);
 insert into department values (4,'HUMAN RESOURCES',25000,13);
 insert into department values (5,'REGULATORY AFFAIRS',5000,null);
 insert into department values (6,'CUSTOMER SERVICE',2000,null);

 insert into employee values (1,'JOHN SMITH',date '1995-01-01','1.123.456.7890',4000.00,1,date '2015-03-28','AC_ACCOUNT','JSMITH');
 insert into employee values (2,'JAMES BOSH',date '1992-02-15','1.234.567.8901',3500.00,2,date '2014-07-01','MK_REP','JBOSH');
 insert into employee values (3,'LUISA JACKSON',date '1970-03-08','1.345.678.9012',4500.00,3,date '2013-08-29','IT_PROG','LJACKSON');
 insert into employee values (4,'STUART GARCIA',date '1965-04-12','1.456.789.0123',2000.00,4,date '2010-02-15','HR_REP','SGARCIA');
 insert into employee values (5,'JUSTIN BLACK',date '1990-05-16','1.567.890.1234',2550.00,1,date '2015-05-02','AC_ACCOUNT','JBLACK');
 insert into employee values (6,'ANGIE CROOD',date '1998-06-22','1.678.901.2345',1500.00,1,date '2015-07-01','AC_ACCOUNT','ACROOD');
 insert into employee values (7,'CHARLES DEAN',date '1973-06-08','1.789.012.3456',2250.00,3,date '2002-03-01','IT_PROG','CDEAN');
 insert into employee values (8,'EDDIE FARREL',date '1980-07-28','1.890.123.4567',3000.00,1,date '2009-04-20','AC_ACCOUNT','EFARREL');
 insert into employee values (9,'GEORGE HAYES',date '1982-08-03',NULL,2500.00,2,date '2012-09-22','MK_REP','GHAYES');
 insert into employee values (10,'IGOR KEYS OSBOURNE',date '1987-09-11','144.898.7564',6000.00,3,date '2014-11-14','IT_PROG','IKEYS');
 insert into employee values (11,'LUKE MINT',date '1985-10-19','1.123.456.7890',5000.00,4,date '2011-01-08','HR_REP','LMINT');
 insert into employee values (12,'NIGEL OAKS',date '1997-11-05','52.987.654.3210',4750.00,4,date '2014-10-01','HR_REP','NOAKS');
 insert into employee values (13,'LUKE GREEN JR',date '1995-02-05',NULL,4750.00,4,date '2015-09-01','HR_REP','LGREEN');
 
CREATE TABLE products
  (
	Product_Id   NUMBER(5),
	Product_Name VARCHAR2(100),
	Price           NUMBER(8,2),
	Expiration_Date DATE
  ) ;
 
ALTER TABLE products ADD CONSTRAINT products_PK PRIMARY KEY ( Product_Id ) ;
 
insert into products values (1,'Aspirin',5,date '2025-12-31');
insert into products values (2,'Penicillin',10,date '2026-04-30');
insert into products values (3,'Insulin',25,date '2026-05-31');
insert into products values (4,'Acetaminophen',5,date '2027-01-31');
insert into products values (5,'Amoxicillin',8,date '2026-07-31');


ALTER TABLE EMPLOYEE ADD BONUS NUMBER;

CREATE TABLE company (
    id                  NUMBER(3) CONSTRAINT pk_company PRIMARY KEY,
    name                VARCHAR2(100) NOT NULL,
    commercial_contact  VARCHAR2(50),
    technical_contact   VARCHAR2(50),
    president           VARCHAR2(50),
    last_contacted      DATE,
    budget              NUMBER(8,2),
    budget_range_start  NUMBER(8,2) NOT NULL,
    budget_range_end    NUMBER(8,2) NOT NULL
);

INSERT INTO company (id,name,commercial_contact,president,budget_range_start,budget_range_end ) VALUES (1,'OUR BRILLIANT FUTURE LTD','LUISA JACKSON','JOHN SMITH',25000,50000);
INSERT INTO company (id,name,president,budget,budget_range_start,budget_range_end ) VALUES (2,'TESTING MAGIC','JUSTIN BLACK',35000,25000,50000);
INSERT INTO company (id,name,technical_contact,president,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (3,'MAKING PROGRESS','ANGIE CROOD','CHARLES DEAN',DATE '2020-01-01',350000,125000,500000);
INSERT INTO company (id,name,commercial_contact,technical_contact,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (4,'SKILL MASTERY','NIGEL OAKS','NIGEL OAKS',DATE '2020-02-15',12000,10000,24000);
INSERT INTO company (id,name,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (5,'UNDECIDED AND CO.',DATE '2015-12-31',51000,51000,100000);

COMMIT;
```


<img width="813" alt="Screen Shot 2022-07-25 at 18 16 12" src="https://user-images.githubusercontent.com/59098085/180875483-6f1a642b-0e74-4efe-a39d-319e6fe9ea81.png">

<img width="1006" alt="Screen Shot 2022-07-25 at 18 16 56" src="https://user-images.githubusercontent.com/59098085/180875579-070bb2dc-2c8c-4485-bb1f-b8e73f6d3700.png">

<img width="367" alt="Screen Shot 2022-07-25 at 18 17 21" src="https://user-images.githubusercontent.com/59098085/180875636-49a23a2d-7d43-47f0-bef5-e0f7df186146.png">


</details> 
</details>

<br/>

### Understanding and Handling NULLs

<br/>

<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
	
<br/>
	
**Comparing NULLs:**	
<p align="justify">The SQL NULL value serves a special purpose. To maintain the integrity of a database, it represents a non-existent value AND an unknown value.</p>

<p align="justify">TSQL uses a Ternary logic. Binary logic uses two values: True and False, 0 and 1, etc. Ternary logic uses three values True, False and Unknown. Because of that, logical operation involving a NULL results in a value of unknown. In this sense, any logical operation involving a NULL results in a value of unknown except for TRUE OR NULL and FALSE AND NULL because the TRUE/FALSE will be valid, but you will be actually testing 'TRUE/FALSE or UNKNOWN'. That means that the only way to compare NULLs correctly is by means of the IS NULL and IS NOT NULL operators. They return only true or false and are the best practice for incorporating NULL values into your queries. </p>

**Operating NULLs:**	
<p align="justify">Be very careful when you perform operations with numeric columns that might contains NULLs. Its better to be forewarned and write the query with that in mind or it might give you problems in the future. Thats because Numeric Value x NULL = Unknown.</p>

</details>

<br/>

#### 📌 C7: The company has a cell phone that is assigned to the employee who is in charge of server support. All employees in the company can do that job, and they switch positions constantly, so the person in charge of support can change at any time, but you can identify it by means of their phone number. The phone number for the server support person is ‘1.234.567.8901’. Your task is to write a query to list ALL employees whose salary is greater than 4000, but you don’t have to include the person currently in charge of server support.

```sql
-- SOLUTION 1
select *
from employee
where salary > 4000
and (phone != '1.234.567.8901'
or phone is null);
```

```sql
-- SOLUTION 2
select *
from employee
where salary > 4000
and LNNVL(phone = '1.234.567.8901');
```

Result:  
<img width="798" alt="Screen Shot 2022-07-25 at 21 07 41" src="https://user-images.githubusercontent.com/59098085/180895306-f0031c59-123a-4d94-8aab-1103a341e9c7.png">


<br/>

### NULL Handling Functions

<br/>

<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
	
<br/>

**NVL vs COALESCE:**	
<p align="justify">The NVL function is Oracle specific and only accepts two expressions as input. If the first expression is null, the function returns the second expression. Otherwise, the first expression will be returned. The input expressions can also be of different types, if this happens an implicit cast attempt will be made, if the cast is not possible an error will be returned. Also, this function always evaluates the two input expressions, making it slightly less performant than COALESCE.Illustration of the NVL function:</p>

![NVL](https://user-images.githubusercontent.com/59098085/181266679-fca576cd-adad-4d13-87ee-7348e9c899ca.gif)

<p align="justify">COALESCE is part of the ANSI-92 standard, so it is a function that exists in all databases that follow this standard or higher. It always returns the first non-null value in the expression list. You must specify at least two expressions, but you can specify more. Illustration of the COALESCE function:</p>

![COALESCE](https://user-images.githubusercontent.com/59098085/181266644-049f5c01-0a06-4455-95d2-351977d4214c.gif)

**NVL vs NVL2:**	
<p align="justify">NVL checks if first argument is null and returns second argument. NVL2 has different logic. If first argument is not null then NVL2 returns second argument, but in other case it will return third argument</p>

</details>

<br/>

#### 📌 C8: Write a query to get a list of companies from the COMPANY table, which includes the following columns. Please define the appropriate aliases so that the columns are shown in the results as mentioned here:
<strong>
COMPANY_NAME

CONTACT_NAME: The commercial contact if we have it. If we don’t have the commercial contact, then return the technical contact. If we don’t have the technical contact, return the president, and if we don’t have the president either, return ‘*NO CONTACT DATA*’.

BUDGET: The budget, if we have it. If we don’t have it, then return the budget range start. Restriction: You must use NVL to generate this column.</strong>

```sql
select 
	name as company_name, 
	coalesce(commercial_contact, technical_contact, president, '*NO CONTACT DATA*') as contact_name, 
	NVL(budget, budget_range_start) as budget
from company;
```

Result:  
<img width="373" alt="Screen Shot 2022-07-25 at 21 09 25" src="https://user-images.githubusercontent.com/59098085/180895435-14f08699-3dce-45e2-b62e-4c83f4e74a37.png">


#### 📌 C9: Someone from our commercial department has been calling the companies stored in the COMPANY table, to confirm if the budgets we have stored are correct, and when that has not been the case, they have immediately made the necessary corrections to the data. As a result, we know that whenever we have any date in the LAST_CONTACTED column, it means that the budget stored in the BUDGET column for that company is correct. If the last_contacted column has NULL, it means we have never contacted that company. Write a query to generate a list of companies with the following information, but don’t include companies we contacted before the year 2019. The companies must be ordered by the last contacted date in ascending order, but companies we have never contacted must appear first.
<strong>
Please make sure that the column names are shown in the results as mentioned here.

COMPANY NAME

EXCLUSIVELY_COMMERCIAL_CONTACT: The commercial contact of the company, but only if it is different from the technical contact. If the commercial contact is the same as the technical contact, then this column must be returned as null.

BUDGET: The budget, but only if we know the value is correct. If we have not confirmed that the budget info we have is correct, then return the budget_range_start.

LAST_CONTACTED_DATE

Restrictions:

1. The use of the logical operators AND/OR is not allowed.

2. You are only allowed to use null-handling functions. No other type of function or expression is allowed in the SELECT list or WHERE clause.
</strong>

```sql
select 
    name as company_name, 
    NULLIF(commercial_contact, technical_contact) as exclusively_commercial_contact, 
    NVL2(last_contacted, budget, budget_range_start) as budget, 
    last_contacted as last_contacted_date
from company
where LNNVL(last_contacted < date '2019-01-01')
order by last_contacted nulls first;
```

Result:  
<img width="606" alt="Screen Shot 2022-07-25 at 21 12 20" src="https://user-images.githubusercontent.com/59098085/180895671-2add4906-2e43-468d-9d4e-56652e5a0a0c.png">


***

## Operators

<br/>

**Content**

- [SQL Operators](#sql-operators)
- [Logical Operators](#logical-operators)
- [Substitution Variables](#substitution-variables)


<br/>

### SQL Operators

<br/>

#### 📌 C10: Write a query to get the list of employees whose name includes the letter “O” 2 times, but not contiguously, so if there was a name “JOHN DOE”, it should be returned, but a row with name “JIM BROOKS” should not, because the 2 Os are contiguous.

Note: Since at this point we still don’t have the necessary knowledge to count the number of ‘O’s that appear in a string, assume that no name will contain more than 2 Os.

```sql
select *
from employee
where name like '%O_%O%';
```

Result:  
<img width="754" alt="Screen Shot 2022-07-27 at 16 24 29" src="https://user-images.githubusercontent.com/59098085/181355284-93f3c6fb-a1b4-4ba0-ace6-fb3eeedc3c62.png">



#### 📌 C11: Write a query to get the list of departments whose monthly budget is greater than 15000 and its name includes a “G” or starts with an “H”, sorted by the department id in descending order.

```sql
select *
from department
where monthly_budget > 15000
and (name like '%G%' 
    or name like 'H_%');
```

Result:  
<img width="438" alt="Screen Shot 2022-07-27 at 16 24 49" src="https://user-images.githubusercontent.com/59098085/181355338-ecfe5888-1228-4125-a3d8-42d60f5fb10c.png">



#### 📌 C12: Write a query to list all employees of the Information Technology and Human Resources departments who earn 3000 or more but not more than 5000. Please include only employees who were born between 1970 and 1990.

```sql
select *
from employee
where department_id in (3,4)
  and salary between 3000 and 5000
  and birthdate between date '1970-01-01' and date '1990-12-31';
```

Result:  
<img width="767" alt="Screen Shot 2022-07-27 at 21 23 13" src="https://user-images.githubusercontent.com/59098085/181394412-0f5f4e95-70b8-4d97-b222-d7d84efa2379.png">


### Logical Operators

<br/>

#### 📌 C13: Write a query to list all employees who were born before 01-jan-1980 or after 01-jan-1995 and earn more than 2000 a month, and whose name does not start or end with an “N”.

When evaluating the condition about how much they earn, please take into account the BONUS column too, which was added with the script provided in the resources section of the lesson about UNDERSTANDING NULLS.

```sql
select *
from employee
where salary + nvl(bonus,0) > 2000
  and
  (birthdate < date '1980-01-01'
    or birthdate > date '1995-01-01')
  and not
  (name like '%N'
    or name like 'N%');
```

Result:  
<img width="741" alt="Screen Shot 2022-07-27 at 21 21 02" src="https://user-images.githubusercontent.com/59098085/181394213-fbbf004a-40ce-4f3d-8ff9-577c74b3a96e.png">


### Substitution Variables

<br/>


Warning: As mentioned in the lesson, the ability to use substitution variables is a feature of SQL Developer (and some other client tools), but this feature is not implemented by Live SQL and Apex, so if you try to run statements with substitution variables there you will get errors.

#### 📌 C14: ~~Write a query to list employees who were hired between a certain range of dates (for example, between January 1st, 2011, and December 15th, 2014). The query must be written in a way that allows the user to use a different date range without needing to modify the query.~~


#### 📌 C15: ~~Write a query to list employees who work in a given department. The query must prompt the user to enter a value, and then return only employees whose salary is equal to the value entered, or equal to the half of the value entered or equal to a third of the value entered by the user.~~

~~The query must also prompt for the id of the department that the user wants to list.~~

~~Your script must include the command necessary to erase the value entered for the salary so that if the query is executed again, the user is prompted for the salary value again.~~


## Group Operations

<br/>

**Content**

- [Aggregate Functions](#aggregate-functions)
	- [Schema #3](#schema-3)
- [Grouping Rows](#grouping-rows)
- [Filtering Groups](#filtering-groups)



<br/>

### Aggregate Functions

<br/>

#### 📌 C16: Write a query to get the number of employees in the Accounting department, the total sum of their salaries, and the average salary. The average must appear 2 times in the results, one of them must be calculated using the AVG function, and one without using the AVG function. Please add column aliases to make it easy to understand the columns in the result.

```sql
select
    count(*) as emps,
    sum(salary) as sum_salary,
    sum(salary)/count(*) as average_salary1,
    avg(salary) as average_salary2
from employee
where department_id = 1;
```

Result:  
<img width="371" alt="Screen Shot 2022-07-27 at 21 31 12" src="https://user-images.githubusercontent.com/59098085/181395160-39f08713-a3ea-4a2e-83d3-724e119a4c99.png">


### Schema #3

<details>
<summary>
Click here to see the script for the tables!
</summary>

```sql

CREATE TABLE department
(
  id	   		number(5) constraint pk_department primary key,
  name	   		varchar2(50),
  monthly_budget 	number(8,2),
  last_employee_id 	number(5)
);

CREATE TABLE employee
(
  id        number(5) constraint pk_employee primary key,
  name      varchar2(50),
  birthdate date,
  phone     varchar2(20),
  salary    number(7,2) not null,
  department_id number(3) constraint fk_employee_department references department,
  hire_date date,
  job_id    varchar2(20),
  email     varchar2(50)
 );


 insert into department values (1,'ACCOUNTING',20000,8);
 insert into department values (2,'MARKETING',15000,9);
 insert into department values (3,'INFORMATION TECHNOLOGY',30000,10);
 insert into department values (4,'HUMAN RESOURCES',25000,13);
 insert into department values (5,'REGULATORY AFFAIRS',5000,null);
 insert into department values (6,'CUSTOMER SERVICE',2000,null);

 insert into employee values (1,'JOHN SMITH',date '1995-01-01','1.123.456.7890',4000.00,1,date '2015-03-28','AC_ACCOUNT','JSMITH');
 insert into employee values (2,'JAMES BOSH',date '1992-02-15','1.234.567.8901',3500.00,2,date '2014-07-01','MK_REP','JBOSH');
 insert into employee values (3,'LUISA JACKSON',date '1970-03-08','1.345.678.9012',4500.00,3,date '2013-08-29','IT_PROG','LJACKSON');
 insert into employee values (4,'STUART GARCIA',date '1965-04-12','1.456.789.0123',2000.00,4,date '2010-02-15','HR_REP','SGARCIA');
 insert into employee values (5,'JUSTIN BLACK',date '1990-05-16','1.567.890.1234',2550.00,1,date '2015-05-02','AC_ACCOUNT','JBLACK');
 insert into employee values (6,'ANGIE CROOD',date '1998-06-22','1.678.901.2345',1500.00,1,date '2015-07-01','AC_ACCOUNT','ACROOD');
 insert into employee values (7,'CHARLES DEAN',date '1973-06-08','1.789.012.3456',2250.00,3,date '2002-03-01','IT_PROG','CDEAN');
 insert into employee values (8,'EDDIE FARREL',date '1980-07-28','1.890.123.4567',3000.00,1,date '2009-04-20','AC_ACCOUNT','EFARREL');
 insert into employee values (9,'GEORGE HAYES',date '1982-08-03',NULL,2500.00,2,date '2012-09-22','MK_REP','GHAYES');
 insert into employee values (10,'IGOR KEYS OSBOURNE',date '1987-09-11','144.898.7564',6000.00,3,date '2014-11-14','IT_PROG','IKEYS');
 insert into employee values (11,'LUKE MINT',date '1985-10-19','1.123.456.7890',5000.00,4,date '2011-01-08','HR_REP','LMINT');
 insert into employee values (12,'NIGEL OAKS',date '1997-11-05','52.987.654.3210',4750.00,4,date '2014-10-01','HR_REP','NOAKS');
 insert into employee values (13,'LUKE GREEN JR',date '1995-02-05',NULL,4750.00,4,date '2015-09-01','HR_REP','LGREEN');
 

CREATE TABLE products
  (
	Product_Id   NUMBER(5),
	Product_Name VARCHAR2(100),
	Price           NUMBER(8,2),
	Expiration_Date DATE
  ) ;
 
ALTER TABLE products ADD CONSTRAINT products_PK PRIMARY KEY ( Product_Id ) ;
 
insert into products values (1,'Aspirin',5,date '2025-12-31');
insert into products values (2,'Penicillin',10,date '2026-04-30');
insert into products values (3,'Insulin',25,date '2026-05-31');
insert into products values (4,'Acetaminophen',5,date '2027-01-31');
insert into products values (5,'Amoxicillin',8,date '2026-07-31');


ALTER TABLE EMPLOYEE ADD BONUS NUMBER;

CREATE TABLE company (
    id                  NUMBER(3) CONSTRAINT pk_company PRIMARY KEY,
    name                VARCHAR2(100) NOT NULL,
    commercial_contact  VARCHAR2(50),
    technical_contact   VARCHAR2(50),
    president           VARCHAR2(50),
    last_contacted      DATE,
    budget              NUMBER(8,2),
    budget_range_start  NUMBER(8,2) NOT NULL,
    budget_range_end    NUMBER(8,2) NOT NULL
);

INSERT INTO company (id,name,commercial_contact,president,budget_range_start,budget_range_end ) VALUES (1,'OUR BRILLIANT FUTURE LTD','LUISA JACKSON','JOHN SMITH',25000,50000);
INSERT INTO company (id,name,president,budget,budget_range_start,budget_range_end ) VALUES (2,'TESTING MAGIC','JUSTIN BLACK',35000,25000,50000);
INSERT INTO company (id,name,technical_contact,president,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (3,'MAKING PROGRESS','ANGIE CROOD','CHARLES DEAN',DATE '2020-01-01',350000,125000,500000);
INSERT INTO company (id,name,commercial_contact,technical_contact,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (4,'SKILL MASTERY','NIGEL OAKS','NIGEL OAKS',DATE '2020-02-15',12000,10000,24000);
INSERT INTO company (id,name,last_contacted,budget,budget_range_start,budget_range_end ) VALUES (5,'UNDECIDED AND CO.',DATE '2015-12-31',51000,51000,100000);

COMMIT;

---
UPDATE employee
SET bonus =
  CASE
    WHEN salary < 3000
    THEN 100
    WHEN salary BETWEEN 3000 AND 4000
    THEN 200
    WHEN salary BETWEEN 4001 AND 4900
    THEN 300
  END;

--
commit;
		    
```
		      
</details>

<img width="810" alt="Screen Shot 2022-07-25 at 18 13 48" src="https://user-images.githubusercontent.com/59098085/180875145-1496f6f2-8701-4b30-9d0e-7012613e6a28.png">
	
<img width="437" alt="Screen Shot 2022-07-25 at 18 14 11" src="https://user-images.githubusercontent.com/59098085/180875195-d4093b09-faa7-4839-add4-48d6ce876552.png">
	
<img width="1010" alt="Screen Shot 2022-07-25 at 18 14 37" src="https://user-images.githubusercontent.com/59098085/180875249-3b413b5f-45a6-487d-9baf-83343bdc158b.png">
	
<img width="367" alt="Screen Shot 2022-07-25 at 18 15 05" src="https://user-images.githubusercontent.com/59098085/180875329-5ee796f1-4dac-4ae4-b95d-527512326bf6.png">

	
### Grouping Rows

<br/>

#### 📌 C17: Write a query to list the different bonuses from the employee table, along with the number of employees that earn that bonus, and the greatest salary for employees in that group. Please include only employees who were born before 1995.

```sql
select 
    nvl(bonus,0) as bonus,
    count(*) as employees,
    max(salary) as max_sal
from employee
where birthdate < to_date('01-01-1995', 'dd-mm-yyyy')
group by nvl(bonus,0)
order by bonus;
```

Result:  
<img width="203" alt="Screen Shot 2022-07-27 at 21 43 50" src="https://user-images.githubusercontent.com/59098085/181396361-94bf4295-d06c-4d35-85eb-dd7820de7dd9.png">
		
### Filtering Groups
**HAVING Clause**

<br/>

#### 📌 C18: Write a query to list the minimum and maximum salaries and also the bonus average per department from the employee table, but please don’t include employees who don’t have a value defined for their bonus.
<strong>
Also, please show in the results only departments whose smallest salary is less than 2000 or their highest salary is greater than 4000. The results must be displayed in descending order by the minimum salary.</strong>

```sql
select 
    department_id,
    min(salary) as min_sal,
    max(salary) as max_sal,
    avg(bonus) as avg_bonus
from employee
where bonus is not null
group by department_id
having min(salary) < 2000
    or max(salary) > 4000
order by min(salary) desc;
```

Result:  
<img width="528" alt="Screen Shot 2022-07-27 at 21 52 49" src="https://user-images.githubusercontent.com/59098085/181397181-e40e976b-c14f-4e2f-b7d2-1c0409cba22d.png">

	
***

<br/>

## Subqueries in SQL

<br/>

<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
	
<br/>
	
**Correlated Subqueries:**
<p align="justify"> Correlated subqueries are used for row-by-row processing. Each subquery is executed once for every row of the outer query. A correlated subquery is one way of reading every row in a table and comparing values in each row against related data. Because the subquery may be evaluated once for each row processed by the outer query, it can be slow. It is used whenever a subquery must return a different result or set of results for each candidate row considered by the outer query (main query). For example, return a value necessary to compare with each employee (aka, a row) as in C3. In this sense, a correlated subquery requires values from its outer query (main query) in order to execute, and if you try to run it separately, you have to substitute at least one of the values. </p>
	
**Non-Correlated Subqueries:**	
<p align="justify">Non-correlated subqueries are those that are totally independent of the main statement. The subquery executes first, and then passes its results to the outer query.</p>
	
**Scalar Subqueries:**	
<p align="justify">A scalar subquery is a subquery expression that can return a maximum of one value and can be either correlated or non-correlated. It is correlated when it returns a single value for each row of its correlated outer table set, as in **C3**. And it is non-correlated when it returns a single value to its containing query, as in C1. </p>
</details>
<br/>

**Content**

- [Subqueries](#subqueries)
- [Inline Views](#inline-views)
- [Subquery Factoring (WITH clause)](#cte) 
- [Top-N Queries](#top-n-queries)
- [Row Limiting Clause](#row-limiting-clause)


<br/>

### Subqueries 

<br/>

#### 📌 C19: Query to display all of the detail of the department where the youngest employee n the company works.


```sql
select *
from department
where department.id = (select department_id
                       from employee
                       where birthdate = (select max(birthdate) 
                                          from employee)
);
```

Result:  
<img width="382" alt="Screen Shot 2022-07-18 at 22 53 46" src="https://user-images.githubusercontent.com/59098085/179647406-289d91d3-fa5d-46dc-b69d-82085e686128.png">

#### 📌 C20: Query to list the names of the departments along with the average salary and the birthdate of the oldest employee that works in each department.

```sql
select d.name, avg(e.salary) as average_salary, max(e.birthdate) as oldest_employee
from department d, employee e
where d.id = e.department_id
group by d.name;
```

Result:  
<img width="408" alt="Screen Shot 2022-07-18 at 22 53 26" src="https://user-images.githubusercontent.com/59098085/179647750-625381af-6aef-4a5d-875e-6a49bc7fca18.png">

#### 📌 C21: Query to list the names of the departments **that exist in the company**, along with the average salary and the birthdate of the oldest employee that works in each department **ordered by department id in descending order**.

```sql
select name, (
    select avg(salary) 
    from employee e 
    where e.department_id = d.id
    ) as average_salary, 
    (
    select min(birthdate) 
    from employee e 
    where e.department_id = d.id
    ) as oldest_employee
from department d
order by d.id desc;
```

Result:  
<img width="405" alt="Screen Shot 2022-07-18 at 22 52 05" src="https://user-images.githubusercontent.com/59098085/179647017-263edb75-367d-403a-91ef-dccba4171dd5.png">


<br/>

### Inline Views

<br/>

#### 📌 C22: Query to list the max, min, and average of salaries for every department id in the employee table, but include only departments whose max salary is greater than the double of their minimum salary.

<strong>RESTRICTION: Not allowed to use a HAVING clause.</strong>

```sql
select *
from ( 
select department_id, max(salary) as max_salary, min(salary) as min_salary, avg(salary) as average_salary
from employee
group by department_id
     ) e
where e.max_salary >= 2*e.min_salary;
```

**This time using the HAVING clause.**

```sql
select department_id, max(salary) as max_salary, min(salary) as min_salary, avg(salary) as average_salary
from employee
group by department_id
having max(salary) >= 2*min(salary);
```

<br/>

### CTE
**a.k.a. Subqueries Factoring or WITH Clause**

<br/>

#### 📌 C23: Query to list the max, min, and average of salaries for every department id in the employee table, but include only departments whose max salary is greater than the double of their minimum salary.
<strong>
This time **using subquery factoring (WITH clause)** instead of an inline view. <br/>
RESTRICTION: Not allowed to use a HAVING clause.</strong>

```sql
with subquery_salary (department_id, max_salary, min_salary, average_salary)
as (
select department_id, max(salary) , min(salary), avg(salary)
from employee
group by department_id
)
select *
from subquery_salary
where max_salary >= 2*min_salary;
```
Result:  
<img width="399" alt="Screen Shot 2022-07-18 at 22 50 04" src="https://user-images.githubusercontent.com/59098085/179646826-cdaba31f-e617-405b-8ca7-806fe99284fe.png">


<br/>

### Top-N Queries

<br/>


#### 📌 C24: Query that uses the rownum pseudocolumn to get the top 5 earners in the employee table.

```sql
with rownumbered as (
    select e.*, row_number() over (order by salary desc) as rn
    from employee e
    order by salary desc
)
select *
from rownumbered
where rn <= 5;
```

Result:  
<img width="780" alt="Screen Shot 2022-07-18 at 23 14 24" src="https://user-images.githubusercontent.com/59098085/179649638-5ae85699-e895-4607-b6d8-94f992d37153.png">

#### 📌 C25: Query that uses the dense_rank analytic function to list the bottom 3 earners in the employee table.

```sql
with rownumbered as (
    select e.*, dense_rank() over (order by salary) as rn
    from employee e
    order by salary
)
select *
from rownumbered
where rn <= 3;
```

Result:  
<img width="747" alt="Screen Shot 2022-07-18 at 23 20 46" src="https://user-images.githubusercontent.com/59098085/179650239-eac18d3f-8d24-4bb4-a9ee-8dfd9ba2d5fc.png">

#### 📌 C26: Use the row limiting clause to write a query to get the top 5 youngest employees among those who earn more than 2000 a month.

WARNING: The row limiting clause was introduced in version 12c.

```sql
with sal as (
select *
from employee
where salary > 2000
)
select *
from sal
order by birthdate desc
fetch first 5 rows only;
```

Result:  
<img width="719" alt="Screen Shot 2022-07-18 at 23 48 48" src="https://user-images.githubusercontent.com/59098085/179653764-90e5ff9a-7031-40db-849f-7b1bc1226673.png">

<br/>

### Row Limiting Clause

<br/>

#### 📌 C27: Query that segments the employee table in pages, based on the salary in ascending order, and returns the third page. The size of each page must be 4 rows.

WARNING: The row limiting clause was introduced in version 12c.

```sql
select *
from employee
order by salary, id
offset (3 - 1) * 4 rows fetch next 4 rows only;

-- If using sql developer, I can replace 3 - 1 for &page -1 to get prompted which page I want
```

Result:  
<img width="712" alt="Screen Shot 2022-07-19 at 14 16 29" src="https://user-images.githubusercontent.com/59098085/179810583-43671351-68f6-4ede-b7d8-601e8a0cb5b5.png">

***


## Single Row Functions

<br/>
<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
	
<br/>
	
**Implicit Conversions:**
<p align="justify">Implicit conversions occur when SQL Server has to do a conversion from one data type to another data type to be able to make a comparison and that conversion wasn't specified in the query. These hidden conversions can be a performance killer, especially if SQL Server has to apply them to every row to perform that comparison. One easy way to see this implicit conversion is with the sql_variant data type. Any comparison to a value that is of that type requires a conversion.</p>

```sql	
/* This requires an implicit conversion, 
because the column 'period' in this example is deined as varchar2 and we are comparing with a number. 
So, oracle applies TO_NUMBER() to the column: */

SELECT *
FROM monthly.account.balance
WHERE period =  201811 and client_id = 100;
```
 
```sql	
/* This does not require an implict conversion. 
Because we are explicitly converting to varchar and it runs 20x faster. */

SELECT *
FROM monthly.account.balance
WHERE period =  '201811' and client_id = 100;
```

</details>

**Content**

- [Text Functions](#text-functions)
- [Numeric Functions](#numeric-functions)
- [Date Functions](#date-functions)
- [Conversion Functions](#conversion-functions)
- [Decode Function and CASE expression](#decode-function-and-case-expression)
- [Date Arithmetic](#date-arithmetic)

<br/>

### Text Functions

<br/>

#### 📌 C28: We need to make some changes to the data about our employees, but before applying the changes we need to see the data as it will be after the changes. Please write a query to list employees data with the following changes:
<strong>
 - The names of all of the employees must be stored with the first letter of each name in uppercase, and the rest of the name in lowercase.
 - The e-mail addresses are incorrect.  All of them must be modified to add “@gmail.com” to the string they currently have, but the current value must be changed to lowercase.
 - Phone numbers have dots, but we want them replaced by hyphens.
 - We need a new column called “CODE” which will be generated by extracting the part of the name that appears before the first blank space, and then removing all vowels from it, so, for an employee called ‘CARLOS’ the code would be ‘CRLS’.</strong>
 
```sql
select id,
  initcap(name) as name,
  birthdate,
  replace(phone,'.','-') as phone,
  salary,
  department_id,
  hire_date,
  job_id,
  lower(email) || '@gmail.com' as email,
  translate(substr(name,1,instr(name,' ')-1),'*AEIOU','*') as code
from employee;
```

Result:  
<img width="878" alt="Screen Shot 2022-07-19 at 20 13 38" src="https://user-images.githubusercontent.com/59098085/179863620-ba0a916c-83c4-4493-b5a6-27b18eebacff.png">

#### 📌 C29: Write a query to generate a list of employees following these requirements:

 - We don’t need the complete phone number. In this report, we only want the numbers that are between the first and second dots, for example, for a number like this 515.123.4567 the report must display ‘123’ only.
 - Please don’t include employees hired before 2010.
 - The report must be ordered by salary, in descending order.
 
```sql
select  id,
  name,
  birthdate,
  phone,
  substr(phone, instr(phone, '.')+1, to_number(instr(phone,'.',1,2) - instr(phone,'.')-1)) as phone,
  salary,
  department_Id,
  hire_date,
  job_id,
  email
from Employee
where hire_date >= to_date('01-01-2010', 'dd-mm-yyyy')
order by salary desc;
```

Result:  
<img width="818" alt="Screen Shot 2022-07-19 at 21 35 24" src="https://user-images.githubusercontent.com/59098085/179870961-cae2543c-f0bb-4ae7-82dd-3b4216ccf621.png">


<br/>

### Numeric Functions

<br/>

#### 📌 C30: Write the query needed to generate a report with the following characteristics. For this task assume that a month has 30 days:
<strong>
- The report must include the names, job_id, salary, daily salary, and the result of applying the round, trunc, ceil and floor functions to the daily salary calculation.

- The report must include only employees whose daily salary is an integer and either were hired after 2010 or work for the ‘IT’ department.
</strong>

```sql
select name, 
       job_id, 
       salary, 
       (salary/30) as daily_salary,
       round(salary/30),
       trunc(salary/30),
       ceil(salary/30),
       floor(salary/30) 
from employee e
where hire_date >= to_date('01-01-2010', 'dd-mm-yyyy')
and MOD((salary/30),1) = 0
or department_id = 3;
```

Result:  
<img width="870" alt="Screen Shot 2022-07-19 at 22 02 01" src="https://user-images.githubusercontent.com/59098085/179873303-3ddef305-5800-40ec-bd0c-0d09ba9bfd13.png">

***

### Date Functions

**Change Date Format on Oracle Live**
<br/>
```sql
alter session set NLS_DATE_FORMAT = 'DD/MM/YYYY HH24:MI:SS';
```
<br/>

#### 📌 C31: Write the query necessary to generate the report with the following characteristics:
<strong>
- The report must include the employee id, name, and hire date.

- It must include a column that tells us for how many months the employee has worked for the company.

- Every employee receives a raise after 6 months of working for the company. Include a column that tells us the date in which they earned the right for the mentioned raise.

- Every employee is sent to a short induction the next Monday after they are hired. Include a column that tells us the date in which they attended their induction.

- Every employee is subscribed to the company’s monthly newsletter on the first day of the next month after they are hired. Add a column that tells us the date in which they were subscribed to the newsletter.

- Do not include employees from the IT department.
</strong>
 
```sql
select
    id,
    name,
    hire_date,
    trunc(months_between(sysdate, hire_date)) as months_worked,
    add_months(hire_date, 6) as raise_earned_date,
    next_day(hire_date, 'monday') as induction_date,
    last_day(hire_date)+1 as newsletter_day
from employee
where department_id != 3;
```

Result:  
<img width="816" alt="Screen Shot 2022-07-20 at 16 30 36" src="https://user-images.githubusercontent.com/59098085/180066272-1c24888a-a07c-4d81-a072-9d37fd56650b.png">


### Conversion Functions
<br/>
<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
	
<br/>
	
**Formating:**
<p align="justify">The format element for minutes is 'MI' and not 'MM'. Careful, using MM will not give any error, it will just mix months in the time portion of your results. This can go unotice for a long time!</p>
</details>

#### 📌 C32: Generate a report of all of the employees who were born after 1970 and for whom we have a phone number registered. In the report, the department_id must be displayed using 4 digits, left-padded with zeros. The salary must be displayed with your local currency symbol and 2 decimals and with commas as the thousands separator.
<strong>
Please add an additional column called “ALT_BIRTHDATE” that will result from swapping the month and day parts of the birthdate, so, for example, if the birthdate is 10-Mar-2015, the alternate birthdate would be 03-Oct-2015 (the day becomes the month and the month becomes the day). If the resulting date is invalid, this column should return NULL.</strong>
 
```sql
select name,birthdate,phone,
  to_char(department_id,'fm0000') as department_id,
  to_char(salary,'fmL99,990.00') as salary,
  to_date(to_char(birthdate,'ddmmyyyy') default null on conversion error,'mmddyyyy') as alt_birthdate
from employee e
where trunc(birthdate, 'yy') >= to_date(1970, 'yyyy')
--where birthdate > to_date('31-12-1969', 'dd-mm-yyyy')
and phone is not null;
```

Result:  
<img width="625" alt="Screen Shot 2022-07-21 at 13 27 46" src="https://user-images.githubusercontent.com/59098085/180265631-96a19f69-204d-4708-9adf-cc0d344bd5ba.png">

#### 📌 C33: Generate a second report that includes all of the employees that were hired before 2015 and earn more than 2500 or were hired in 2015 but earn less than 3000. The report must include the employees’ names, the day and month of the birthdate, and only the month (name of the month) and year of the hire date.
<strong>
The company is planning to give every employee a surprise bonus for the amount of the last 4 digits of their phone number, so please include an additional column that displays the amount of this bonus for every employee. This amount must be displayed with your local currency symbol and 2 decimals.

They will receive this surprise bonus in the month that corresponds to the last digit of their phone number, so, for example, if the employee’s phone number ends with a 4, it means that he must receive his bonus in April. Please include an additional column that tells us the name of the month in which they must receive their bonus. If any employee has a phone number that ends in a number that is not a valid month, they must receive their bonus in December.</strong>
 
```sql
select 
    name,
    to_char(birthdate,'dd/mm') as birthdate,
    to_char(hire_date,'fmMonth yyyy') as hire_date,
    to_char(to_number(substr(phone,-4)),'L9990.00') as bonus,
    to_char(to_date(substr(phone,-1) default '12' on conversion error,'mm'),'Month') as bonus_month
from employee
where trunc(hire_date, 'yyyy') < to_date('01-01-2015', 'dd-mm-yyyy') and salary > 2500
or trunc(hire_date, 'yyyy') = to_date('01-01-2015', 'dd-mm-yyyy') and salary < 3000;
```

Result:  
<img width="561" alt="Screen Shot 2022-07-21 at 14 37 10" src="https://user-images.githubusercontent.com/59098085/180277929-02281bd4-4ccd-48b0-9351-063dec5db2d3.png">


### Decode Function and CASE expression
<br/>
<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
<br/>
	
**Decode vs Case:**
	- Decode is exclusive of oracle and less readable than CASE expressions.

</details>


#### 📌 C34: The company wants to give a rise to all employees according to these conditions:
<strong>
- Employees who work in the ACCOUNTING department get a 10% increase to their salary.

- Employees who work in the MARKETING department get a 15% increase to their salary.

- Employees from the other departments get a 20% increase to their salary.

Please generate a report that includes the employee id, name, current salary, and new salary. Please generate 2 columns for the new salary. To calculate the first one use the DECODE function and for the second one use a simple CASE expression. The result in both new salary columns must be the same.
 </strong>

```sql
select
    id,
    name,
    salary as current_salary,
    salary + (salary * decode(department_id,1,0.10,2,0.15,0.20)) as new_salary_1,
    salary + (salary * 
    case 
        when department_id = 1
            then 0.1
        when department_id = 2
            then 2
        else 3
    end) as new_salary_2
from employee;
```

Result:  
<img width="485" alt="Screen Shot 2022-07-21 at 20 17 31" src="https://user-images.githubusercontent.com/59098085/180330559-80b3fc41-256c-4d7b-b7b0-4bde25f248d4.png">


#### 📌 C35: The company is planning to assign a classification to each employee based on the salary they earn. The classification would be as follows:
<strong>
- Employees who earn less than 2500 will be classified as “A”.

- Employees who earn 2500 or more but less than 4000 will be classified as “B”.

- Employees who earn 4000 or more will be classified as “C” if they were hired before 2014 and will be classified as “D” if they were hired in 2014 or 2015.

Please generate a report that includes the employee id, name, salary, the year they were hired, and the classification of each employee, but don’t include employees from the MARKETING department, and also don’t include employees who don’t have a phone number registered. The report must be ordered by salary and hire_date.</strong>
 
```sql
select
    id,
    name,
    salary,
    extract(year from hire_date) as hire_year,
    case
        when salary < 2500
            then 'A'
        when salary >= 2500 and salary < 4000
            then 'B'
        when salary >= 4000 and extract(year from hire_date) < 2014
            then 'C'
        when salary >= 4000 and extract(year from hire_date) >= 2014 and extract(year from hire_date) <= 2015
            then 'D'
        else 'not categorized'
    end as classification
from employee
where department_id != 2
  and phone is not null
order by salary,hire_date;
```

Result:  
<img width="426" alt="Screen Shot 2022-07-21 at 20 35 37" src="https://user-images.githubusercontent.com/59098085/180332025-c8d8138a-d16e-471e-80d9-9677d7272118.png">


### Date Arithmetic

<br/>

#### 📌 C36: Write an employees report with the following columns:
<strong>
- Id

- Name

- Date of their second birthday (don’t use functions to calculate this date, and assume that all years have 365 days (ignore the possibility of leap years), so the result will actually be an approximation of the second birthday date.)

- How old they were when they were hired. Their age must be expressed in hours (not years).

Please include only employees who were hired in 1980 or later and whose phone number starts with “1”. Order results by department id (ascending) and salary (descending).</strong>
 
```sql
select
    id,
    name,
    birthdate+(2*365) as second_birthday,
    (hire_date - birthdate) * 24 as hours_old_when_hired
from employee
where hire_date >= date '1980-01-01'
and phone like '1%'
order by department_id,salary desc;
```

Result:  
<img width="446" alt="Screen Shot 2022-07-21 at 20 58 45" src="https://user-images.githubusercontent.com/59098085/180334125-05be3126-d21a-465e-8272-a87f6a86a979.png">


***

## Transposing

<br/>

**Content**

- [Pivot](#pivot)
- [Unpivot](#unpivot)

<br/>

### Pivot

<details> 
<summary>
Click here for an interesting example given by the teacher. 🔑</p>
	
</summary>

#### 📌 Interesting Example: Write a query that tells the number of employees hired in the years of 2014 and 2015 for each department. First example is made in traditional way, second example is made using pivot clause.
 
```sql
select 
    department_id,
    count( 
            case to_char(hire_date, 'YYYY')
            when '2014' then 1
            end ) as "2014",
    count( 
            case to_char(hire_date, 'YYYY')
            when '2015' then 1
            end ) as "2015"
from employee
group by department_id
order by department_id;
```

<br/>

```sql
select *
from 
(
select department_id, to_char(hire_date, 'YYYY') as year
from employee
)
pivot (count(*) for year in (2014, 2015))
order by department_id;
```

Result:  
<img width="203" alt="Screen Shot 2022-07-22 at 23 00 08" src="https://user-images.githubusercontent.com/59098085/180586243-47813f56-4be4-41fa-9018-ac7672428c61.png">

<br/>
	
</details>

#### 📌 C37: Write a query that returns a single row that has one column for each of the monthly budgets of the departments ACCOUNTING, MARKETING, and INFORMATION TECHNOLOGY. The column titles for the budgets must be the names of the departments.
 
```sql
select *
from 
(
select name, monthly_budget
from department
)
pivot(
max(monthly_budget) for name in ('ACCOUNTING', 'MARKETING','INFORMATION TECHNOLOGY')
);
```
  
<details> 
<summary>
Why MAX()?</p>
	
</summary>
<br/>
	
**Why MAX()?**

<p align="justify">You need an aggregate function. Depending on what you want to do, it could be MAX, MIN, AVG, etc…

Sometimes you don’t want to aggregate anything, because you are working with a single row for each value. In those cases, you can use some function like MAX or MIN just to comply with the requirement of using an aggregate function, but because there is only one row for each value, the results would be correct.</p>

</details>

Result:  
<img width="378" alt="Screen Shot 2022-07-22 at 23 20 46" src="https://user-images.githubusercontent.com/59098085/180586950-c4e2705e-7055-4686-88a3-81d5d1c075f8.png">

### Unpivot

<br/>

#### 📌 C38: Write a query to generate a list of employees who work in the Accounting and Marketing departments. The report must include the name, birthdate, and hire_date, but each employee must appear in the report 2 times, and the birth date and hire date must appear in the same column but in different rows. This column must be called “date_value” and there must be an additional column that explains the kind of date that is included in the date_value column. This additional column must be called “date_type” and will contain either “Date of Birth” or “Date of Hiring”.
 
```sql
select name,date_type,date_value
from employee
  unpivot
  ( 
    date_value for 
    date_type in (birthdate as 'Date of Birth', hire_date as 'Date of Hiring')
  )
  where department_id in (1, 2);
```

Result:  
<img width="301" alt="Screen Shot 2022-07-22 at 23 40 26" src="https://user-images.githubusercontent.com/59098085/180587562-9e69d93d-df56-4864-b479-8a3797ac2bb5.png">

***

## Analytic Functions

<br/>
<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
<br/>
	
**Aggregate Functions vs Analytic Functions:** <br/>
<p align="justify">Aggregate functions (count, avg, sum, min, max, etc..) perform a calculation on a set of values and return a single value. Analytic functions compute an aggregate value based on a set of values, and, unlike aggregate functions, can return multiple rows for each set of values. Aggregate functions can be used as analytic function when you use the windows function (over() clause) since can return multiple rows.</p>

</details>


**Content**

- [Partition Clause](#partition-clause)
- [Window Function](#window-function)
- [Common Analytic Functions](#common-analytic-functions)
- [Ranking Functions](#ranking-functions)
- [LISTAGG Function](#listagg-function)
- [LAG and LEAD Functions](#lag-and-lead-functions)
- [FIRST and LAST Functions](#first-and-last-functions)
- [FIRST_VALUE and LAST_VALUE Functions](#first_value-and-last_value-functions)

<br/>

### Partition Clause

<br/>

#### 📌 C39: Write a query to generate a list of employees with the following characteristics:
<strong>
· All employees must be returned.

· The report must include the following columns from the table: Id, name, department_id, email.

· The report must also include the following calculated columns: The length of the email. The number of employees from the same department who have an email of the same length.

· The report must be ordered by department_id and length of the email column.</strong>


```sql
select 
    id,
    name,
    department_id,
    email,
    length(email) as length_email,
    count(*) over (partition by (length(email)), department_id) as CNT_elength
from employee
order by department_id, length_email;
```

Result:  
<img width="538" alt="Screen Shot 2022-07-23 at 16 36 19" src="https://user-images.githubusercontent.com/59098085/180620391-53ff5240-2340-43e5-aceb-9be6548ee4b7.png">


### Window Function

<br/>
<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
<br/>
	
**What is a Window Function?** <br/>
<p align="justify">A window functions perform calculations over a set of rows (known as a “window”) and return a single value for each row from the underlying query. A window (or windowing or windowed) function makes use of the values from the rows in a window to calculate the returned values. When you use a window function in a query, define the window using the OVER() clause. The OVER() clause (window definition) differentiates window functions from other analytical and reporting functions. A query can include multiple window functions with the same or different window definitions. If a function has an OVER clause, then it is a window function. If it lacks an OVER clause, then it is an ordinary aggregate or scalar function. Window functions might also have a FILTER clause in between the function and the OVER clause.</p>

Named window-defn clauses may also be added to a SELECT statement using a WINDOW clause and then referred to by name within window function invocations. For example, the following SELECT statement contains two named window-defs clauses, "win1" and "win2":

```sql
SELECT x, y, row_number() OVER win1, rank() OVER win2 
FROM t0 
WINDOW win1 AS (ORDER BY y RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW),
       win2 AS (PARTITION BY y ORDER BY x)
ORDER BY x;
```
	
**Partition Clause vs Window Function:** <br/>
<p align="justify">Partition is static, once you define the partition it does not change. But the windows can change or move as we process diferent rows. In this sense, when used together, windows move inside the partitions.</p>
</details>


#### 📌 C40: Write a query to generate a report of the employees, which includes at least the following columns:
<strong>
· Id

· Name

· Hire_date,

· A count of the number of employees hired in the same year of the current employee or in the previous year.

The results must be ordered by the hire date.</strong>
 
```sql
-- SOLUTION 1
select
    id,
    name,
    department_id,
    salary,
    hire_date,
    count(*) over(
    order by to_number(to_char(hire_date, 'yyyy'))
    range 1 preceding
    ) as counts
from employee;

-- SOLUTION 2
select
    id,
    name,
    department_id,
    salary,
    hire_date,
    count(*) over(
    order by extract(year from hire_date)
    range 1 preceding
    ) as counts
from employee;
```

Result:  
<img width="474" alt="Screen Shot 2022-07-24 at 17 38 17" src="https://user-images.githubusercontent.com/59098085/180664982-96074ac7-3750-4970-b40e-cbbeaff83fbc.png">


### Common Analytic Functions
- **Observation:** The course author is refering to sum, count, min, max, etc.. when used with over(). Since they can return multiple rows for each set of values, they become analytic functions by definition.

<br/>

#### 📌 C41: Write a query to generate a list of all of the departments including their ID, name, and monthly budget, but also include a column that shows the accumulated budget (the sum of the budget of previous departments plus the current one). To decide the order in which the budgets are accumulated you must sort them by smallest to greatest budget.
 
```sql
select 
    id,
    name,
    monthly_budget,
    sum(monthly_budget) over (order by monthly_budget) as accumulated_mb
from department;
```

Result:  
<img width="432" alt="Screen Shot 2022-07-24 at 17 52 58" src="https://user-images.githubusercontent.com/59098085/180665457-5d3841fd-5ccb-43b2-ac81-300128782cbc.png">


### Ranking Functions

<details> 
<summary>
Click here for study notes on key concepts. 🔑</p>
	
</summary>
<br/>
	
**ROW_NUMBER vs DENSE_RANK vs RANK:** <br/>
<p align="justify">The row_number() function numbers the rows 1,2,3,etc by the columns in the ORDER BY clause, and if there are ties, it is arbitrary which rows that gets the same number. The difference between rank() and dense_rank() functions comes down to how they handle identical values. The rank() and dense_rank() will give the same ranking to rows that cannot be distinguished by the order by clause, but dense_rank will always generate a contiguous sequence of ranks like (1,2,3,etc), whereas rank() will leave gaps after two or more rows with the same rank (1,2,2,4,etc).</p>

</details>

<br/>

#### 📌 C42: Write a query to list all the employees. The result must include their name, department id, hire date, and a column called “hire_order” which is a number that indicates the order in which they were hired. This order is related to the department where they work only, so, the first employee that was hired in each department will have a hire_order of 1.
 
```sql
with hire_order as (
select 
    name,
    department_id,
    hire_date,
    rank() over (partition by department_id order by hire_date) as rn
from employee
)
select *
from hire_order; 
```

Result:  
<img width="362" alt="Screen Shot 2022-07-25 at 10 52 43" src="https://user-images.githubusercontent.com/59098085/180793932-45ddfd09-8590-4732-ac98-41771a24b0bc.png">


#### 📌 C43: Write a query that returns the name, birthdate, and department id of an employee who was born in 1995, preferably from the ACCOUNTING department. If no employee from that department was born in 1995, return one from any other department.
 
```sql
with prioritized as (
select 
    name,
    birthdate,
    department_id,
    row_number() over (order by case 
                                    when department_id = 1 then 'A'
                                    else 'B'
                                end) as rn
from employee
where to_char(birthdate, 'YYYY') = 1995
)
select *
from prioritized
where rn = 1;   
```

Result:  
<img width="308" alt="Screen Shot 2022-07-25 at 10 59 33" src="https://user-images.githubusercontent.com/59098085/180795333-c9c10d52-14bf-467b-a2a3-cc6881a37bbf.png">


### LISTAGG Function

<br/>

#### 📌 C44: Write a query that lists the different salaries that appear in the employee table. For each salary include a comma-separated list of the names of the employees that earn that amount. The list of employees for each salary must be ordered by the name of the employee, and the final result set must be ordered by salary from greatest to smallest.
 
```sql
select
    salary,
    listagg(name, ',') within group (order by name) as emplist
from employee
group by salary
order by salary desc;
```

Result:  
<img width="248" alt="Screen Shot 2022-07-25 at 11 08 20" src="https://user-images.githubusercontent.com/59098085/180797112-31539621-d7d7-4ef5-9ef7-bfebc59dbe6b.png">


### LAG and LEAD Functions

<br/>

#### 📌 C45: Write a query to generate a list of all employees from the ACCOUNTING and HUMAN RESOURCES departments, ordered by department and birthdate. For every employee, the report must include the name, birthdate, and the name of the employee from the same department who follows him/her if you order them by age.
 
```sql
select
    name,
    birthdate,
    lead(name) over(partition by department_id order by birthdate desc) as next_by_age
from employee
where department_id = 1 or department_id = 4
-- where department_id in (1,4)
order by department_id, birthdate;
```

Result:  
<img width="296" alt="Screen Shot 2022-07-25 at 11 22 03" src="https://user-images.githubusercontent.com/59098085/180799890-dd11c674-6c61-46c8-82e2-efe95ef54188.png">


#### 📌 C46: Write a query to generate a list of employees with the following conditions:
<strong>
· The list must include only the employee with the highest salary in each department.

· It must include ID, name, salary, department_id, and an additional column with the ID of the employee with the second-highest salary in his/her department.

· Hint: You might need to use some kind of subquery.</strong>

```sql
-- SOLUTION BY ME
with tab_max_salary as (
select 
    e.*,
    max(salary) over(partition by department_id) as max_salary,
    lead(id) over(partition by department_id order by salary desc) as next_by_salary
from employee e
)
select 
    id,
    name,
    birthdate,
    salary,
    department_id,
    next_by_salary
from tab_max_salary
where salary = max_salary;
```

```sql
-- SOLUTION BY THE TEACHER
SELECT id, name, salary, department_id,employee_with_2nd_highest
FROM
   (
      SELECT id, name, salary, department_id, 
         ROW_NUMBER() over (PARTITION BY department_id ORDER BY salary DESC) AS rn,
         LEAD(ID) over (PARTITION BY department_id ORDER BY salary DESC) AS employee_with_2nd_highest
      FROM employee
   )
WHERE rn = 1;
```

Result:  
<img width="527" alt="Screen Shot 2022-07-25 at 11 52 34" src="https://user-images.githubusercontent.com/59098085/180806584-691a9063-31c5-4038-9756-340600084399.png">


### FIRST and LAST Functions

<br/>

#### 📌 C47: Write a query to return the name and hire date of the first employee hired in each department. The results must include the department_id, name of the employee and their hire date, and must be ordered by department id.
 
```sql
select 
    department_id,
    max (name) keep (dense_rank first order by hire_date) as name,
    min (hire_date) as hire_date
from employee
group by department_id
order by department_id;
```

Result:  
<img width="293" alt="Screen Shot 2022-07-25 at 16 13 01" src="https://user-images.githubusercontent.com/59098085/180856298-1d93e461-9cec-48e1-bd15-35c05ec34bd6.png">


### FIRST_VALUE and LAST_VALUE Functions

<br/>

#### 📌 C48: Write a query that will produce an employees’ report with the following information for each employee:
<strong>
· Id, name, and department_id of the employee.

· Name of the employee who was the first hire in the department where the employee works.

· Salary of the employee who was the first hire in the department where the employee works.

· Bonus of the top earner among the employees who were hired in the same year as the employee, regardless of their department. If the bonus is null, the bonus must be shown as 0.

The report must be ordered by department_id and hire_date.</strong>
 
```sql
select
    id,
    name,
    department_id,
    first_value(name) over(partition by department_id order by hire_date) as fv_hire,
    first_value(salary) over(partition by department_id order by hire_date) as fv_salary,
    nvl(last_value(bonus) over(partition by to_char(hire_date,'YYYY') order by salary
            rows between unbounded preceding and unbounded following), 0) as top_earner_bonus
from employee e
order by department_id, hire_date;
```

Result:  
<img width="586" alt="Screen Shot 2022-07-25 at 18 44 09" src="https://user-images.githubusercontent.com/59098085/180879093-ef5acf3d-9ec4-4a24-a614-5665164a026e.png">

***

## Set Operators

<br/>


**Content**

- [UNION and UNION ALL Operators](#union-and-union-all-operators)
- [INTERSECT Operator](#intersect-operator)
- [MINUS Operator](#minus-operator)
- [Combining Set Operators in the Same Query](#combining-set-operators-in-the-same-query)

<br/>

### UNION and UNION ALL Operators

<br/>

#### 📌 C49: The company wants to send a congratulations letter to employees who were born in the months of May or June, and they also want to send a letter to employees who were hired by the company in those months.

<strong>Please write a query to generate the list of employees that have to receive the letters mentioned in the previous paragraph.

The list only needs to include the Id, name, birthdate, and hire_date. Nothing more.

If an employee complies with the conditions to receive both letters, he/she has to be included in the report twice.

Please order the report by employee id.</strong>


```sql
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from birthdate) in(5,6)
union all
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from hire_date) in(5,6)
order by id;
```

Result:  
<img width="293" alt="Screen Shot 2022-07-29 at 12 33 02" src="https://user-images.githubusercontent.com/59098085/181793824-2065801e-9a12-4784-ab2c-2ef254a1bce1.png">


### INTERSECT Operator

<br/>

#### 📌 C50: Using the same description of the task from the previous lecture, write a compound query to generate the list of employees that should get the 2 letters. Every employee needs to appear only once in this report.

<strong>The list only needs to include the Id, name, birthdate, and hire_date. Nothing more.

Reference Description:

The company wants to send a congratulations letter to employees who were born in the months of May or June, and they also want to send a letter to employees who were hired by the company in those months.</strong>


```sql
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from birthdate) in(5,6)
intersect
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from hire_date) in(5,6)
order by id;
```

Result:  
<img width="289" alt="Screen Shot 2022-07-29 at 12 37 10" src="https://user-images.githubusercontent.com/59098085/181794556-fc14d057-1f5c-4734-8f35-8db8f88f9466.png">



### MINUS Operator

<br/>

#### 📌 C51: Using the same description of the task from the previous lecture, write a compound query to generate the list of employees that should get the first letter but not the second one.

<strong>The list only needs to include the Id, name, birthdate, and hire_date. Nothing more.

Reference Description:

The company wants to send a congratulations letter to employees who were born in the months of May or June, and they also want to send a letter to employees who were hired by the company in those months.</strong>



```sql
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from birthdate) in(5,6)
minus
select
    id,
    name,
    birthdate,
    hire_date
from employee
where extract(month from hire_date) in(5,6)
order by id;
```

Result:  
<img width="290" alt="Screen Shot 2022-07-29 at 12 41 05" src="https://user-images.githubusercontent.com/59098085/181795224-c3292281-e787-42ce-b505-6352084ccb55.png">



### Combining Set Operators in the Same Query

<br/>

#### 📌 C52: The company classifies employees who earn more than 3000 as “trusted employees”. This classification, however, does not apply to employees of the IT department. Write a query to list trusted employees that were hired in 2015.

<strong>Restrictions:

You must use SET operators

Each component query can have only one single condition in its WHERE clause (the use of ANDs and ORs is not allowed).</strong>



```sql
select
    id,
    name,
    salary,
    hire_date
from employee
where salary > 3000
minus
select
    id,
    name,
    salary,
    hire_date
from employee
where department_id = 3
intersect
select
    id,
    name,
    salary,
    hire_date
from employee
where to_char(hire_date, 'yyyy') = 2015;
```

Result:  
<img width="284" alt="Screen Shot 2022-07-29 at 12 47 33" src="https://user-images.githubusercontent.com/59098085/181796408-0487fafe-7086-498c-a9d9-bada37438d9e.png">


## Selecting data from multiple tables

<br/>


**Content**

- [Introduction to SQL Joins](#introduction-to-sql-joins)
- [More Complex Schema](#more-complex-schema)
- [Inner Joins](#inner-joins)
- [Other Types of Joins](#other-types-of-joins)


<br/>

### Introduction to SQL Joins

<br/>

#### 📌 C53: Write a query to list the names of the departments along with the number of employees and the sum of salaries for each one.


```sql
select 
    d.name,
    count(e.name) as emplo,
    sum(salary) as sum_salary
from employee e
join department d
on d.id = e.department_id
group by d.name
order by emplo desc;
```

Result:  
<img width="310" alt="Screen Shot 2022-07-31 at 15 28 44" src="https://user-images.githubusercontent.com/59098085/182040224-5c9d65e7-2dbf-4eec-8dec-08e11953cc61.png">



### More Complex Schema

<br/>
<details>
<summary>
Click here to see the script for the tables!
</summary>

**To run in ORACLE LIVE I had to devide the query in 3 parts. For some reason ORACLE LIVE does not accepted everything at once.**

```sql
--Removing old tables
DROP TABLE employee;
DROP TABLE department;

--------------------------------------------------------
--  DDL for Table COUNTRIES
--------------------------------------------------------

  CREATE TABLE "COUNTRIES" ("COUNTRY_ID" CHAR(2), "COUNTRY_NAME" VARCHAR2(40), "REGION_ID" NUMBER,  CONSTRAINT "COUNTRY_C_ID_PK" PRIMARY KEY ("COUNTRY_ID") ENABLE);

   COMMENT ON COLUMN "COUNTRIES"."COUNTRY_ID" IS 'Primary key of countries table.';
   COMMENT ON COLUMN "COUNTRIES"."COUNTRY_NAME" IS 'Country name';
   COMMENT ON COLUMN "COUNTRIES"."REGION_ID" IS 'Region ID for the country. Foreign key to region_id column in the departments table.';
   COMMENT ON TABLE "COUNTRIES"  IS 'country table. Contains 25 rows. References with locations table.';
--------------------------------------------------------
--  DDL for Table DEPARTMENTS
--------------------------------------------------------

  CREATE TABLE "DEPARTMENTS" ("DEPARTMENT_ID" NUMBER(4,0), "DEPARTMENT_NAME" VARCHAR2(30), "MANAGER_ID" NUMBER(6,0), "LOCATION_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "DEPARTMENTS"."DEPARTMENT_ID" IS 'Primary key column of departments table.';
   COMMENT ON COLUMN "DEPARTMENTS"."DEPARTMENT_NAME" IS 'A not null column that shows name of a department. Administration,
Marketing, Purchasing, Human Resources, Shipping, IT, Executive, Public
Relations, Sales, Finance, and Accounting. ';
   COMMENT ON COLUMN "DEPARTMENTS"."MANAGER_ID" IS 'Manager_id of a department. Foreign key to employee_id column of employees table. The manager_id column of the employee table references this column.';
   COMMENT ON COLUMN "DEPARTMENTS"."LOCATION_ID" IS 'Location id where a department is located. Foreign key to location_id column of locations table.';
   COMMENT ON TABLE "DEPARTMENTS"  IS 'Departments table that shows details of departments where employees
work. Contains 27 rows; references with locations, employees, and job_history tables.';
--------------------------------------------------------
--  DDL for Table EMPLOYEES
--------------------------------------------------------

  CREATE TABLE "EMPLOYEES" ("EMPLOYEE_ID" NUMBER(6,0), "FIRST_NAME" VARCHAR2(20), "LAST_NAME" VARCHAR2(25), "EMAIL" VARCHAR2(25), "PHONE_NUMBER" VARCHAR2(20), "HIRE_DATE" DATE, "JOB_ID" VARCHAR2(10), "SALARY" NUMBER(8,2), "COMMISSION_PCT" NUMBER(2,2), "MANAGER_ID" NUMBER(6,0), "DEPARTMENT_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "EMPLOYEES"."EMPLOYEE_ID" IS 'Primary key of employees table.';
   COMMENT ON COLUMN "EMPLOYEES"."FIRST_NAME" IS 'First name of the employee. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."LAST_NAME" IS 'Last name of the employee. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."EMAIL" IS 'Email id of the employee';
   COMMENT ON COLUMN "EMPLOYEES"."PHONE_NUMBER" IS 'Phone number of the employee; includes country code and area code';
   COMMENT ON COLUMN "EMPLOYEES"."HIRE_DATE" IS 'Date when the employee started on this job. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."JOB_ID" IS 'Current job of the employee; foreign key to job_id column of the
jobs table. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."SALARY" IS 'Monthly salary of the employee. Must be greater
than zero (enforced by constraint emp_salary_min)';
   COMMENT ON COLUMN "EMPLOYEES"."COMMISSION_PCT" IS 'Commission percentage of the employee; Only employees in sales
department elgible for commission percentage';
   COMMENT ON COLUMN "EMPLOYEES"."MANAGER_ID" IS 'Manager id of the employee; has same domain as manager_id in
departments table. Foreign key to employee_id column of employees table.
(useful for reflexive joins and CONNECT BY query)';
   COMMENT ON COLUMN "EMPLOYEES"."DEPARTMENT_ID" IS 'Department id where employee works; foreign key to department_id
column of the departments table';
   COMMENT ON TABLE "EMPLOYEES"  IS 'employees table. Contains 107 rows. References with departments,
jobs, job_history tables. Contains a self reference.';
--------------------------------------------------------
--  DDL for Table JOB_HISTORY
--------------------------------------------------------

  CREATE TABLE "JOB_HISTORY" ("EMPLOYEE_ID" NUMBER(6,0), "START_DATE" DATE, "END_DATE" DATE, "JOB_ID" VARCHAR2(10), "DEPARTMENT_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "JOB_HISTORY"."EMPLOYEE_ID" IS 'A not null column in the complex primary key employee_id+start_date.
Foreign key to employee_id column of the employee table';
   COMMENT ON COLUMN "JOB_HISTORY"."START_DATE" IS 'A not null column in the complex primary key employee_id+start_date.
Must be less than the end_date of the job_history table. (enforced by
constraint jhist_date_interval)';
   COMMENT ON COLUMN "JOB_HISTORY"."END_DATE" IS 'Last day of the employee in this job role. A not null column. Must be
greater than the start_date of the job_history table.
(enforced by constraint jhist_date_interval)';
   COMMENT ON COLUMN "JOB_HISTORY"."JOB_ID" IS 'Job role in which the employee worked in the past; foreign key to
job_id column in the jobs table. A not null column.';
   COMMENT ON COLUMN "JOB_HISTORY"."DEPARTMENT_ID" IS 'Department id in which the employee worked in the past; foreign key to deparment_id column in the departments table';
   COMMENT ON TABLE "JOB_HISTORY"  IS 'Table that stores job history of the employees. If an employee
changes departments within the job or changes jobs within the department,
new rows get inserted into this table with old job information of the
employee. Contains a complex primary key: employee_id+start_date.
Contains 25 rows. References with jobs, employees, and departments tables.';
--------------------------------------------------------
--  DDL for Table JOBS
--------------------------------------------------------

  CREATE TABLE "JOBS" ("JOB_ID" VARCHAR2(10), "JOB_TITLE" VARCHAR2(35), "MIN_SALARY" NUMBER(6,0), "MAX_SALARY" NUMBER(6,0)) ;

   COMMENT ON COLUMN "JOBS"."JOB_ID" IS 'Primary key of jobs table.';
   COMMENT ON COLUMN "JOBS"."JOB_TITLE" IS 'A not null column that shows job title, e.g. AD_VP, FI_ACCOUNTANT';
   COMMENT ON COLUMN "JOBS"."MIN_SALARY" IS 'Minimum salary for a job title.';
   COMMENT ON COLUMN "JOBS"."MAX_SALARY" IS 'Maximum salary for a job title';
   COMMENT ON TABLE "JOBS"  IS 'jobs table with job titles and salary ranges. Contains 19 rows.
References with employees and job_history table.';
--------------------------------------------------------
--  DDL for Table LOCATIONS
--------------------------------------------------------

  CREATE TABLE "LOCATIONS" ("LOCATION_ID" NUMBER(4,0), "STREET_ADDRESS" VARCHAR2(40), "POSTAL_CODE" VARCHAR2(12), "CITY" VARCHAR2(30), "STATE_PROVINCE" VARCHAR2(25), "COUNTRY_ID" CHAR(2)) ;

   COMMENT ON COLUMN "LOCATIONS"."LOCATION_ID" IS 'Primary key of locations table';
   COMMENT ON COLUMN "LOCATIONS"."STREET_ADDRESS" IS 'Street address of an office, warehouse, or production site of a company.
Contains building number and street name';
   COMMENT ON COLUMN "LOCATIONS"."POSTAL_CODE" IS 'Postal code of the location of an office, warehouse, or production site
of a company. ';
   COMMENT ON COLUMN "LOCATIONS"."CITY" IS 'A not null column that shows city where an office, warehouse, or
production site of a company is located. ';
   COMMENT ON COLUMN "LOCATIONS"."STATE_PROVINCE" IS 'State or Province where an office, warehouse, or production site of a
company is located.';
   COMMENT ON COLUMN "LOCATIONS"."COUNTRY_ID" IS 'Country where an office, warehouse, or production site of a company is
located. Foreign key to country_id column of the countries table.';
   COMMENT ON TABLE "LOCATIONS"  IS 'Locations table that contains specific address of a specific office,
warehouse, and/or production site of a company. Does not store addresses /
locations of customers. Contains 23 rows; references with the
departments and countries tables. ';
--------------------------------------------------------
--  DDL for Table REGIONS
--------------------------------------------------------

  CREATE TABLE "REGIONS" ("REGION_ID" NUMBER, "REGION_NAME" VARCHAR2(25));
REM INSERTING into COUNTRIES
--SET DEFINE OFF;
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('AR','Argentina',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('AU','Australia',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('BE','Belgium',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('BR','Brazil',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CA','Canada',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CH','Switzerland',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CN','China',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('DE','Germany',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('DK','Denmark',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('EG','Egypt',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('FR','France',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IL','Israel',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IN','India',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IT','Italy',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('JP','Japan',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('KW','Kuwait',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ML','Malaysia',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('MX','Mexico',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('NG','Nigeria',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('NL','Netherlands',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('SG','Singapore',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('UK','United Kingdom',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('US','United States of America',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ZM','Zambia',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ZW','Zimbabwe',4);
REM INSERTING into DEPARTMENTS
--SET DEFINE OFF;
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (10,'Administration',200,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (20,'Marketing',201,1800);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (30,'Purchasing',114,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (40,'Human Resources',203,2400);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (50,'Shipping',121,1500);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (60,'IT',103,1400);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (70,'Public Relations',204,2700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (80,'Sales',145,2500);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (90,'Executive',100,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (100,'Finance',108,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (110,'Accounting',205,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (120,'Treasury',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (130,'Corporate Tax',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (140,'Control And Credit',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (150,'Shareholder Services',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (160,'Benefits',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (170,'Manufacturing',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (180,'Construction',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (190,'Contracting',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (200,'Operations',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (210,'IT Support',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (220,'NOC',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (230,'IT Helpdesk',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (240,'Government Sales',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (250,'Retail Sales',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (260,'Recruiting',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (270,'Payroll',null,1700);
REM INSERTING into EMPLOYEES
--SET DEFINE OFF;
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (100,'Steven','King','SKING','515.123.4567',to_date('17-JUN-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AD_PRES',24000,null,null,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (101,'Neena','Kochhar','NKOCHHAR','515.123.4568',to_date('21-SEP-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AD_VP',17000,null,100,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (102,'Lex','De Haan','LDEHAAN','515.123.4569',to_date('13-JAN-2001','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AD_VP',17000,null,100,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (103,'Alexander','Hunold','AHUNOLD','590.423.4567',to_date('03-JAN-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',9000,null,102,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (104,'Bruce','Ernst','BERNST','590.423.4568',to_date('21-MAY-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',6000,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (105,'David','Austin','DAUSTIN','590.423.4569',to_date('25-JUN-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',4800,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (106,'Valli','Pataballa','VPATABAL','590.423.4560',to_date('05-FEB-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',4800,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (107,'Diana','Lorentz','DLORENTZ','590.423.5567',to_date('07-FEB-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',4200,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (108,'Nancy','Greenberg','NGREENBE','515.124.4569',to_date('17-AUG-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_MGR',12008,null,101,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (109,'Daniel','Faviet','DFAVIET','515.124.4169',to_date('16-AUG-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_ACCOUNT',9000,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (110,'John','Chen','JCHEN','515.124.4269',to_date('28-SEP-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_ACCOUNT',8200,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (111,'Ismael','Sciarra','ISCIARRA','515.124.4369',to_date('30-SEP-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_ACCOUNT',7700,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (112,'Jose Manuel','Urman','JMURMAN','515.124.4469',to_date('07-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_ACCOUNT',7800,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (113,'Luis','Popp','LPOPP','515.124.4567',to_date('07-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'FI_ACCOUNT',6900,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (114,'Den','Raphaely','DRAPHEAL','515.127.4561',to_date('07-DEC-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_MAN',11000,null,100,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (115,'Alexander','Khoo','AKHOO','515.127.4562',to_date('18-MAY-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_CLERK',3100,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (116,'Shelli','Baida','SBAIDA','515.127.4563',to_date('24-DEC-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_CLERK',2900,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (117,'Sigal','Tobias','STOBIAS','515.127.4564',to_date('24-JUL-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_CLERK',2800,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (118,'Guy','Himuro','GHIMURO','515.127.4565',to_date('15-NOV-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_CLERK',2600,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (119,'Karen','Colmenares','KCOLMENA','515.127.4566',to_date('10-AUG-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PU_CLERK',2500,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (120,'Matthew','Weiss','MWEISS','650.123.1234',to_date('18-JUL-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_MAN',8000,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (121,'Adam','Fripp','AFRIPP','650.123.2234',to_date('10-APR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_MAN',8200,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (122,'Payam','Kaufling','PKAUFLIN','650.123.3234',to_date('01-MAY-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_MAN',7900,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (123,'Shanta','Vollman','SVOLLMAN','650.123.4234',to_date('10-OCT-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_MAN',6500,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (124,'Kevin','Mourgos','KMOURGOS','650.123.5234',to_date('16-NOV-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_MAN',5800,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (125,'Julia','Nayer','JNAYER','650.124.1214',to_date('16-JUL-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (126,'Irene','Mikkilineni','IMIKKILI','650.124.1224',to_date('28-SEP-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2700,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (127,'James','Landry','JLANDRY','650.124.1334',to_date('14-JAN-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2400,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (128,'Steven','Markle','SMARKLE','650.124.1434',to_date('08-MAR-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (129,'Laura','Bissot','LBISSOT','650.124.5234',to_date('20-AUG-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3300,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (130,'Mozhe','Atkinson','MATKINSO','650.124.6234',to_date('30-OCT-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2800,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (131,'James','Marlow','JAMRLOW','650.124.7234',to_date('16-FEB-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2500,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (132,'TJ','Olson','TJOLSON','650.124.8234',to_date('10-APR-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2100,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (133,'Jason','Mallin','JMALLIN','650.127.1934',to_date('14-JUN-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3300,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (134,'Michael','Rogers','MROGERS','650.127.1834',to_date('26-AUG-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2900,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (135,'Ki','Gee','KGEE','650.127.1734',to_date('12-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2400,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (136,'Hazel','Philtanker','HPHILTAN','650.127.1634',to_date('06-FEB-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2200,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (137,'Renske','Ladwig','RLADWIG','650.121.1234',to_date('14-JUL-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3600,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (138,'Stephen','Stiles','SSTILES','650.121.2034',to_date('26-OCT-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3200,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (139,'John','Seo','JSEO','650.121.2019',to_date('12-FEB-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2700,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (140,'Joshua','Patel','JPATEL','650.121.1834',to_date('06-APR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2500,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (141,'Trenna','Rajs','TRAJS','650.121.8009',to_date('17-OCT-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3500,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (142,'Curtis','Davies','CDAVIES','650.121.2994',to_date('29-JAN-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',3100,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (143,'Randall','Matos','RMATOS','650.121.2874',to_date('15-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (144,'Peter','Vargas','PVARGAS','650.121.2004',to_date('09-JUL-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',2500,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (145,'John','Russell','JRUSSEL','011.44.1344.429268',to_date('01-OCT-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',14000,0.4,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (146,'Karen','Partners','KPARTNER','011.44.1344.467268',to_date('05-JAN-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',13500,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (147,'Alberto','Errazuriz','AERRAZUR','011.44.1344.429278',to_date('10-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',12000,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (148,'Gerald','Cambrault','GCAMBRAU','011.44.1344.619268',to_date('15-OCT-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',11000,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (149,'Eleni','Zlotkey','EZLOTKEY','011.44.1344.429018',to_date('29-JAN-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',10500,0.2,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (150,'Peter','Tucker','PTUCKER','011.44.1344.129268',to_date('30-JAN-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',10000,0.3,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (151,'David','Bernstein','DBERNSTE','011.44.1344.345268',to_date('24-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9500,0.25,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (152,'Peter','Hall','PHALL','011.44.1344.478968',to_date('20-AUG-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9000,0.25,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (153,'Christopher','Olsen','COLSEN','011.44.1344.498718',to_date('30-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',8000,0.2,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (154,'Nanette','Cambrault','NCAMBRAU','011.44.1344.987668',to_date('09-DEC-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7500,0.2,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (155,'Oliver','Tuvault','OTUVAULT','011.44.1344.486508',to_date('23-NOV-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7000,0.15,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (156,'Janette','King','JKING','011.44.1345.429268',to_date('30-JAN-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',10000,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (157,'Patrick','Sully','PSULLY','011.44.1345.929268',to_date('04-MAR-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9500,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (158,'Allan','McEwen','AMCEWEN','011.44.1345.829268',to_date('01-AUG-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9000,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (159,'Lindsey','Smith','LSMITH','011.44.1345.729268',to_date('10-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',8000,0.3,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (160,'Louise','Doran','LDORAN','011.44.1345.629268',to_date('15-DEC-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7500,0.3,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (161,'Sarath','Sewall','SSEWALL','011.44.1345.529268',to_date('03-NOV-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7000,0.25,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (162,'Clara','Vishney','CVISHNEY','011.44.1346.129268',to_date('11-NOV-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',10500,0.25,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (163,'Danielle','Greene','DGREENE','011.44.1346.229268',to_date('19-MAR-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9500,0.15,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (164,'Mattea','Marvins','MMARVINS','011.44.1346.329268',to_date('24-JAN-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7200,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (165,'David','Lee','DLEE','011.44.1346.529268',to_date('23-FEB-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',6800,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (166,'Sundar','Ande','SANDE','011.44.1346.629268',to_date('24-MAR-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',6400,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (167,'Amit','Banda','ABANDA','011.44.1346.729268',to_date('21-APR-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',6200,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (168,'Lisa','Ozer','LOZER','011.44.1343.929268',to_date('11-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',11500,0.25,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (169,'Harrison','Bloom','HBLOOM','011.44.1343.829268',to_date('23-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',10000,0.2,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (170,'Tayler','Fox','TFOX','011.44.1343.729268',to_date('24-JAN-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',9600,0.2,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (171,'William','Smith','WSMITH','011.44.1343.629268',to_date('23-FEB-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7400,0.15,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (172,'Elizabeth','Bates','EBATES','011.44.1343.529268',to_date('24-MAR-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7300,0.15,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (173,'Sundita','Kumar','SKUMAR','011.44.1343.329268',to_date('21-APR-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',6100,0.1,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (174,'Ellen','Abel','EABEL','011.44.1644.429267',to_date('11-MAY-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',11000,0.3,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (175,'Alyssa','Hutton','AHUTTON','011.44.1644.429266',to_date('19-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',8800,0.25,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (176,'Jonathon','Taylor','JTAYLOR','011.44.1644.429265',to_date('24-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',8600,0.2,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (177,'Jack','Livingston','JLIVINGS','011.44.1644.429264',to_date('23-APR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',8400,0.2,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (178,'Kimberely','Grant','KGRANT','011.44.1644.429263',to_date('24-MAY-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',7000,0.15,149,null);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (179,'Charles','Johnson','CJOHNSON','011.44.1644.429262',to_date('04-JAN-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',6200,0.1,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (180,'Winston','Taylor','WTAYLOR','650.507.9876',to_date('24-JAN-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (181,'Jean','Fleaur','JFLEAUR','650.507.9877',to_date('23-FEB-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3100,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (182,'Martha','Sullivan','MSULLIVA','650.507.9878',to_date('21-JUN-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2500,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (183,'Girard','Geoni','GGEONI','650.507.9879',to_date('03-FEB-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2800,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (184,'Nandita','Sarchand','NSARCHAN','650.509.1876',to_date('27-JAN-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',4200,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (185,'Alexis','Bull','ABULL','650.509.2876',to_date('20-FEB-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',4100,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (186,'Julia','Dellinger','JDELLING','650.509.3876',to_date('24-JUN-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3400,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (187,'Anthony','Cabrio','ACABRIO','650.509.4876',to_date('07-FEB-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3000,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (188,'Kelly','Chung','KCHUNG','650.505.1876',to_date('14-JUN-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3800,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (189,'Jennifer','Dilly','JDILLY','650.505.2876',to_date('13-AUG-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3600,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (190,'Timothy','Gates','TGATES','650.505.3876',to_date('11-JUL-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2900,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (191,'Randall','Perkins','RPERKINS','650.505.4876',to_date('19-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2500,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (192,'Sarah','Bell','SBELL','650.501.1876',to_date('04-FEB-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',4000,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (193,'Britney','Everett','BEVERETT','650.501.2876',to_date('03-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3900,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (194,'Samuel','McCain','SMCCAIN','650.501.3876',to_date('01-JUL-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3200,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (195,'Vance','Jones','VJONES','650.501.4876',to_date('17-MAR-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2800,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (196,'Alana','Walsh','AWALSH','650.507.9811',to_date('24-APR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3100,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (197,'Kevin','Feeney','KFEENEY','650.507.9822',to_date('23-MAY-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',3000,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (198,'Donald','OConnell','DOCONNEL','650.507.9833',to_date('21-JUN-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (199,'Douglas','Grant','DGRANT','650.507.9844',to_date('13-JAN-2008','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SH_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (200,'Jennifer','Whalen','JWHALEN','515.123.4444',to_date('17-SEP-2003','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AD_ASST',4400,null,101,10);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (201,'Michael','Hartstein','MHARTSTE','515.123.5555',to_date('17-FEB-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'MK_MAN',13000,null,100,20);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (202,'Pat','Fay','PFAY','603.123.6666',to_date('17-AUG-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'MK_REP',6000,null,201,20);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (203,'Susan','Mavris','SMAVRIS','515.123.7777',to_date('07-JUN-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'HR_REP',6500,null,101,40);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (204,'Hermann','Baer','HBAER','515.123.8888',to_date('07-JUN-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'PR_REP',10000,null,101,70);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (205,'Shelley','Higgins','SHIGGINS','515.123.8080',to_date('07-JUN-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AC_MGR',12008,null,101,110);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (206,'William','Gietz','WGIETZ','515.123.8181',to_date('07-JUN-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AC_ACCOUNT',8300,null,205,110);
REM INSERTING into JOB_HISTORY
--SET DEFINE OFF;
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (102,to_date('13-JAN-2001','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('24-JUL-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'IT_PROG',60);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (101,to_date('21-SEP-1997','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('27-OCT-2001','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AC_ACCOUNT',110);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (101,to_date('28-OCT-2001','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('15-MAR-2005','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AC_MGR',110);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (201,to_date('17-FEB-2004','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('19-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'MK_REP',20);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (114,to_date('24-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('31-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',50);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (122,to_date('01-JAN-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('31-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'ST_CLERK',50);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (200,to_date('17-SEP-1995','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('17-JUN-2001','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AD_ASST',90);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (176,to_date('24-MAR-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('31-DEC-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_REP',80);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (176,to_date('01-JAN-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('31-DEC-2007','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'SA_MAN',80);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (200,to_date('01-JUL-2002','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),to_date('31-DEC-2006','DD-MON-YYYY','NLS_DATE_LANGUAGE = ''english'''),'AC_ACCOUNT',90);
REM INSERTING into JOBS
--SET DEFINE OFF;
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_PRES','President',20080,40000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_VP','Administration Vice President',15000,30000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_ASST','Administration Assistant',3000,6000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('FI_MGR','Finance Manager',8200,16000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('FI_ACCOUNT','Accountant',4200,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AC_MGR','Accounting Manager',8200,16000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AC_ACCOUNT','Public Accountant',4200,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SA_MAN','Sales Manager',10000,20080);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SA_REP','Sales Representative',6000,12008);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PU_MAN','Purchasing Manager',8000,15000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PU_CLERK','Purchasing Clerk',2500,5500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('ST_MAN','Stock Manager',5500,8500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('ST_CLERK','Stock Clerk',2008,5000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SH_CLERK','Shipping Clerk',2500,5500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('IT_PROG','Programmer',4000,10000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('MK_MAN','Marketing Manager',9000,15000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('MK_REP','Marketing Representative',4000,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('HR_REP','Human Resources Representative',4000,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PR_REP','Public Relations Representative',4500,10500);
REM INSERTING into LOCATIONS
--SET DEFINE OFF;
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1000,'1297 Via Cola di Rie','00989','Roma',null,'IT');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1100,'93091 Calle della Testa','10934','Venice',null,'IT');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1200,'2017 Shinjuku-ku','1689','Tokyo','Tokyo Prefecture','JP');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1300,'9450 Kamiya-cho','6823','Hiroshima',null,'JP');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1400,'2014 Jabberwocky Rd','26192','Southlake','Texas','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1500,'2011 Interiors Blvd','99236','South San Francisco','California','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1600,'2007 Zagora St','50090','South Brunswick','New Jersey','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1700,'2004 Charade Rd','98199','Seattle','Washington','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1800,'147 Spadina Ave','M5V 2L7','Toronto','Ontario','CA');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1900,'6092 Boxwood St','YSW 9T2','Whitehorse','Yukon','CA');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2000,'40-5-12 Laogianggen','190518','Beijing',null,'CN');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2100,'1298 Vileparle (E)','490231','Bombay','Maharashtra','IN');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2200,'12-98 Victoria Street','2901','Sydney','New South Wales','AU');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2300,'198 Clementi North','540198','Singapore',null,'SG');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2400,'8204 Arthur St',null,'London',null,'UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2500,'Magdalen Centre, The Oxford Science Park','OX9 9ZB','Oxford','Oxford','UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2600,'9702 Chester Road','09629850293','Stretford','Manchester','UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2700,'Schwanthalerstr. 7031','80925','Munich','Bavaria','DE');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2800,'Rua Frei Caneca 1360 ','01307-002','Sao Paulo','Sao Paulo','BR');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2900,'20 Rue des Corps-Saints','1730','Geneva','Geneve','CH');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3000,'Murtenstrasse 921','3095','Bern','BE','CH');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3100,'Pieter Breughelstraat 837','3029SK','Utrecht','Utrecht','NL');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3200,'Mariano Escobedo 9991','11932','Mexico City','Distrito Federal,','MX');
REM INSERTING into REGIONS
--SET DEFINE OFF;
Insert into REGIONS (REGION_ID,REGION_NAME) values (1,'Europe');
Insert into REGIONS (REGION_ID,REGION_NAME) values (2,'Americas');
Insert into REGIONS (REGION_ID,REGION_NAME) values (3,'Asia');
Insert into REGIONS (REGION_ID,REGION_NAME) values (4,'Middle East and Africa');
--------------------------------------------------------
--  DDL for Index DEPT_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "DEPT_ID_PK" ON "DEPARTMENTS" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index DEPT_LOCATION_IX
--------------------------------------------------------

  CREATE INDEX "DEPT_LOCATION_IX" ON "DEPARTMENTS" ("LOCATION_ID");
--------------------------------------------------------
--  DDL for Index EMP_EMAIL_UK
--------------------------------------------------------

  CREATE UNIQUE INDEX "EMP_EMAIL_UK" ON "EMPLOYEES" ("EMAIL");
--------------------------------------------------------
--  DDL for Index EMP_EMP_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "EMP_EMP_ID_PK" ON "EMPLOYEES" ("EMPLOYEE_ID");
--------------------------------------------------------
--  DDL for Index EMP_DEPARTMENT_IX
--------------------------------------------------------

  CREATE INDEX "EMP_DEPARTMENT_IX" ON "EMPLOYEES" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index EMP_JOB_IX
--------------------------------------------------------

  CREATE INDEX "EMP_JOB_IX" ON "EMPLOYEES" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index EMP_MANAGER_IX
--------------------------------------------------------

  CREATE INDEX "EMP_MANAGER_IX" ON "EMPLOYEES" ("MANAGER_ID");
--------------------------------------------------------
--  DDL for Index EMP_NAME_IX
--------------------------------------------------------

  CREATE INDEX "EMP_NAME_IX" ON "EMPLOYEES" ("LAST_NAME", "FIRST_NAME");
--------------------------------------------------------
--  DDL for Index JHIST_EMP_ID_ST_DATE_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "JHIST_EMP_ID_ST_DATE_PK" ON "JOB_HISTORY" ("EMPLOYEE_ID", "START_DATE");
--------------------------------------------------------
--  DDL for Index JHIST_JOB_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_JOB_IX" ON "JOB_HISTORY" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index JHIST_EMPLOYEE_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_EMPLOYEE_IX" ON "JOB_HISTORY" ("EMPLOYEE_ID");
--------------------------------------------------------
--  DDL for Index JHIST_DEPARTMENT_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_DEPARTMENT_IX" ON "JOB_HISTORY" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index JOB_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "JOB_ID_PK" ON "JOBS" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index LOC_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "LOC_ID_PK" ON "LOCATIONS" ("LOCATION_ID");
--------------------------------------------------------
--  DDL for Index LOC_CITY_IX
--------------------------------------------------------

  CREATE INDEX "LOC_CITY_IX" ON "LOCATIONS" ("CITY");
--------------------------------------------------------
--  DDL for Index LOC_STATE_PROVINCE_IX
--------------------------------------------------------

  CREATE INDEX "LOC_STATE_PROVINCE_IX" ON "LOCATIONS" ("STATE_PROVINCE");
--------------------------------------------------------
--  DDL for Index LOC_COUNTRY_IX
--------------------------------------------------------

  CREATE INDEX "LOC_COUNTRY_IX" ON "LOCATIONS" ("COUNTRY_ID");
--------------------------------------------------------
--  DDL for Index REG_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "REG_ID_PK" ON "REGIONS" ("REGION_ID");
--------------------------------------------------------
--  Constraints for Table COUNTRIES
--------------------------------------------------------

  ALTER TABLE "COUNTRIES" MODIFY ("COUNTRY_ID" CONSTRAINT "COUNTRY_ID_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table DEPARTMENTS
--------------------------------------------------------

  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_ID_PK" PRIMARY KEY ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "DEPARTMENTS" MODIFY ("DEPARTMENT_NAME" CONSTRAINT "DEPT_NAME_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table EMPLOYEES
--------------------------------------------------------

  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_EMP_ID_PK" PRIMARY KEY ("EMPLOYEE_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_EMAIL_UK" UNIQUE ("EMAIL") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_SALARY_MIN" CHECK (salary > 0) ENABLE;
  ALTER TABLE "EMPLOYEES" MODIFY ("JOB_ID" CONSTRAINT "EMP_JOB_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("HIRE_DATE" CONSTRAINT "EMP_HIRE_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("EMAIL" CONSTRAINT "EMP_EMAIL_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("LAST_NAME" CONSTRAINT "EMP_LAST_NAME_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table JOB_HISTORY
--------------------------------------------------------

  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_EMP_ID_ST_DATE_PK" PRIMARY KEY ("EMPLOYEE_ID", "START_DATE") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_DATE_INTERVAL" CHECK (end_date > start_date) ENABLE;
  ALTER TABLE "JOB_HISTORY" MODIFY ("JOB_ID" CONSTRAINT "JHIST_JOB_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("END_DATE" CONSTRAINT "JHIST_END_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("START_DATE" CONSTRAINT "JHIST_START_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("EMPLOYEE_ID" CONSTRAINT "JHIST_EMPLOYEE_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table JOBS
--------------------------------------------------------

  ALTER TABLE "JOBS" ADD CONSTRAINT "JOB_ID_PK" PRIMARY KEY ("JOB_ID") ENABLE;
  ALTER TABLE "JOBS" MODIFY ("JOB_TITLE" CONSTRAINT "JOB_TITLE_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table LOCATIONS
--------------------------------------------------------

  ALTER TABLE "LOCATIONS" ADD CONSTRAINT "LOC_ID_PK" PRIMARY KEY ("LOCATION_ID") ENABLE;
  ALTER TABLE "LOCATIONS" MODIFY ("CITY" CONSTRAINT "LOC_CITY_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table REGIONS
--------------------------------------------------------

  ALTER TABLE "REGIONS" ADD CONSTRAINT "REG_ID_PK" PRIMARY KEY ("REGION_ID") ENABLE;
  ALTER TABLE "REGIONS" MODIFY ("REGION_ID" CONSTRAINT "REGION_ID_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Ref Constraints for Table COUNTRIES
--------------------------------------------------------

  ALTER TABLE "COUNTRIES" ADD CONSTRAINT "COUNTR_REG_FK" FOREIGN KEY ("REGION_ID") REFERENCES "REGIONS" ("REGION_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table DEPARTMENTS
--------------------------------------------------------

  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_LOC_FK" FOREIGN KEY ("LOCATION_ID") REFERENCES "LOCATIONS" ("LOCATION_ID") ENABLE;
  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_MGR_FK" FOREIGN KEY ("MANAGER_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table EMPLOYEES
--------------------------------------------------------

  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_DEPT_FK" FOREIGN KEY ("DEPARTMENT_ID") REFERENCES "DEPARTMENTS" ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_JOB_FK" FOREIGN KEY ("JOB_ID") REFERENCES "JOBS" ("JOB_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_MANAGER_FK" FOREIGN KEY ("MANAGER_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table JOB_HISTORY
--------------------------------------------------------

  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_DEPT_FK" FOREIGN KEY ("DEPARTMENT_ID") REFERENCES "DEPARTMENTS" ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_EMP_FK" FOREIGN KEY ("EMPLOYEE_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_JOB_FK" FOREIGN KEY ("JOB_ID") REFERENCES "JOBS" ("JOB_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table LOCATIONS
--------------------------------------------------------

  ALTER TABLE "LOCATIONS" ADD CONSTRAINT "LOC_C_ID_FK" FOREIGN KEY ("COUNTRY_ID") REFERENCES "COUNTRIES" ("COUNTRY_ID") ENABLE;
```

</details>
<img width="290" alt="Screen Shot 2022-08-04 at 09 39 53" src="https://user-images.githubusercontent.com/59098085/182849230-c0b46190-8146-480f-be7a-34ce6cd27267.png">
<img width="295" alt="Screen Shot 2022-08-04 at 09 40 17" src="https://user-images.githubusercontent.com/59098085/182849306-ca60ce81-aac7-4b12-9132-5da96658891d.png">
<img width="264" alt="Screen Shot 2022-08-04 at 09 40 42" src="https://user-images.githubusercontent.com/59098085/182849383-9402798f-ad11-491d-b977-02f1644cda87.png">
<img width="281" alt="Screen Shot 2022-08-04 at 09 41 09" src="https://user-images.githubusercontent.com/59098085/182849442-2c52997a-9106-4df1-bd54-bc6af04ef80d.png">
<img width="290" alt="Screen Shot 2022-08-04 at 09 42 00" src="https://user-images.githubusercontent.com/59098085/182849593-49085226-10ca-4c7e-b469-4702d280ee54.png">
<img width="275" alt="Screen Shot 2022-08-04 at 09 42 23" src="https://user-images.githubusercontent.com/59098085/182849678-36b2a7f9-094d-4213-90e9-b02de974f639.png">
<img width="269" alt="Screen Shot 2022-08-04 at 09 42 42" src="https://user-images.githubusercontent.com/59098085/182849741-b747a797-3a4b-4ea0-a1c7-f3338a07d56a.png">


<br/>

#### 📌 C54: Write a query to list the IDs names and salary of all employees that work in the Finance department, along with their job titles.


```sql
select 
    e.employee_id,
    e.first_name,
    e.last_name,
    e.salary,
    j.job_title
from employees e
join jobs j 
on e.job_id = j.job_id
where e.department_id = 100;
```

Result:  
<img width="441" alt="Screen Shot 2022-07-31 at 16 43 05" src="https://user-images.githubusercontent.com/59098085/182042542-9c602ed2-0ac2-4fdc-acd6-7813d1cbac0f.png">


### Inner Joins

<br/>

#### 📌 C55: Write a query to list the ID, name, and salary of all employees who don't work in the 'IT' department, along with their job titles and the name of the department where they work. Please write a version using the new standard syntax, another version using the “short hand” for the standard syntax, and another version using the old method to write join queries.


```sql
select 
    e.employee_id,
    e.first_name,
    e.last_name,
    e.salary,
    j.job_title,
    d.department_name
from employees e
join jobs j 
on e.job_id = j.job_id
join departments d
on d.department_id = e.department_id
where e.department_id != 60
order by employee_id
--offset 0 rows fetch next 15 rows only;
```

Result:  
<img width="658" alt="Screen Shot 2022-07-31 at 17 05 39" src="https://user-images.githubusercontent.com/59098085/182043271-f7ffce5d-e305-423a-b5e4-09f624920d08.png">



### Other Types of Joins

<br/>

#### 📌 C56: Write a query that returns a list of employees that includes the employee id, name, and salary along with the name of their manager.

<strong>Remember that in the EMPLOYEES table, the column “manager_id” corresponds to the employee_id of another employee who works as a manager. So if you see an employee with manager_id = 100, it means that in the same EMPLOYEES table, there is an employee whose employee_id is 100, who works as a manager.</strong>


```sql
select 
    e1.employee_id,
    e1.first_name,
    e1.last_name,
    e1.salary,
    e1.manager_id,
    e2.first_name as mgr_fn,
    e2.last_name as mgr_ln
from employees e1
join employees e2
on e1.manager_id = e2.employee_id
order by employee_id
--offset 0 rows fetch next 15 rows only;
```

Result:  
<img width="566" alt="Screen Shot 2022-07-31 at 17 34 11" src="https://user-images.githubusercontent.com/59098085/182044253-3f707a7e-bc00-4d2e-acb7-40548d6636ae.png">


## Hierarchical Queries

<br/>


**Content**

- [Hierarchical Query Clause](#hierarchical-query-clause)
- [Hierarchical Pseudo-Columns](#hierarchical-pseudo-columns)
- [Hierarchical Operators and Functions](#hierarchical-operators-and-functions)
- [Understanding The Execution of Hierarchical Queries](#understanding-the-execution-of-hierarchical-queries)
- [Sorting The Results of Hierarchical Queries](#sorting-the-results-of-hierarchical-queries)


<br/>

### Hierarchical Query Clause

<br/>

#### 📌 C57: Using your employees table, write a query to generate a report of all of the employees, which includes the following columns: Employee id, first name, last name, and job id of the employee plus first name, last name, and job id of their direct manager. Order the results by employee id.

```sql
select 
    employee_id,
    first_name,
    last_name,
    salary,
    job_id,
    prior first_name as mgr_fn,
    prior last_name as mgr_ln,
    prior job_id as mgr_job_id
from employees
start with manager_id is null
connect by manager_id = prior employee_id
--offset 0 rows fetch next 15 rows only;
```

Result:  
<img width="631" alt="Screen Shot 2022-08-01 at 10 50 31" src="https://user-images.githubusercontent.com/59098085/182162879-c921378a-dc0b-46a6-9295-5d6e27762d0c.png">



### Hierarchical Pseudo-Columns

<br/>

#### 📌 C58: Write a hierarchical query from your employees table, in which you include employees whose level in the hierarchy is greater than 2 or don’t have any child. Order the results by their level in descending order.


```sql
select 
    employee_id,
    first_name,
    last_name,
    manager_id,
    level,
    connect_by_isleaf
from employees
where level > 2 or connect_by_isleaf = 1
start with manager_id is null
connect by manager_id = prior employee_id
order by level desc
--offset 0 rows fetch next 15 rows only;
```

Result:  
<img width="531" alt="Screen Shot 2022-08-01 at 11 03 13" src="https://user-images.githubusercontent.com/59098085/182165457-a3e06d4b-490b-4416-865e-e8aa6e03545c.png">


### Hierarchical Operators and Functions

<br/>

#### 📌 C59: Write a query to list the employees that are part of the hierarchy tree for which employee ‘Neena Kochhar’ is the root. The list must include the employee id, first name, last name, and the hierarchy path, which should be built using the employee id, separating levels with a slash.

```sql
select 
    employee_id,
    first_name,
    last_name,
    sys_connect_by_path(employee_id, '->') as path
from employees
start with employee_id = 101
connect by manager_id = prior employee_id
order by level;
```

Result:  
<img width="387" alt="Screen Shot 2022-08-01 at 11 17 51" src="https://user-images.githubusercontent.com/59098085/182168308-4d2208ff-e89e-4c2b-ae4e-c5f45c4df555.png">



#### 📌 C60: Write a query to list every manager from the employees table, along with the number of employees who report to him/her directly or indirectly. The list must include 3 columns:
<strong>
1) The employee id

2) The whole name of the employee, which would be built concatenating the first and last names separated by a blank space

3) The number of employees that report to him/her directly or indirectly.

HINT: You might need to use a subquery. </strong>

```sql
with hierarchy as (
            select
                employee_id,
                connect_by_root employee_id as root_id,
                connect_by_root first_name || ' ' || connect_by_root last_name as root_name
                -- connect_by_root (first_name || ' ' || last_name) as root_name
            from employees
            connect by prior employee_id = manager_id
)
select 
        root_id,
        root_name,
        count(*) as employees
from hierarchy
where employee_id != root_id
group by root_id, 
         root_name
order by employees desc;
```

Result:  
<img width="282" alt="Screen Shot 2022-08-03 at 18 49 57" src="https://user-images.githubusercontent.com/59098085/182718718-589643df-e03d-4cec-990b-6e9f9f1194af.png">


<br/>
<p align="center"><strong> Elaborating a little more this exercise.</p></strong>

```sql
with hierarchy as (
             select  employee_id,
                   first_name,
                   last_name,
                   sys_connect_by_path(employee_id,',') || ',' path,
                   level as lvl
                   --rownum rn
             from  employees
             start with manager_id  is null
             connect by manager_id = prior employee_id
          )
select  lpad(' ',min(t2.lvl)) || t1.first_name || ' ' || t1.last_name as emp_idented,
        t1.lvl,
        count(*) - 1 as hierarchy_cnt
from  hierarchy t1,
      hierarchy t2
where t2.path like '%,' || t1.employee_id || ',%'
having count(*) - 1 != 0
group by t1.employee_id,
         t1.first_name,
         t1.last_name,
         t1.lvl
         --t1.rn
order by count(*) - 1 desc;
```

Result:  
<img width="294" alt="Screen Shot 2022-08-03 at 18 41 34" src="https://user-images.githubusercontent.com/59098085/182717654-15c89db1-b38a-40e3-9f03-11da7d5ee0d0.png">



### Understanding The Execution of Hierarchical Queries

<br/>

#### 📌 C61: Write a query to display the rows that are part of the hierarchy of the employee with last name ‘Urman’, which includes the employee id, last name, department name, hierarchy path (built with the last name), and level. The hierarchy should be built starting with employee ‘Urman’ upwards to ‘King’, so Urman must be level 1 and King level 4.


```sql
select 
    employee_id,
    last_name,
    department_name,
    sys_connect_by_path(last_name, '->') as path,
    level
from employees e
join departments d
on d.department_id = e.department_id
start with last_name = 'Urman'
connect by prior e.manager_id = e.employee_id
order by level;
```

Result:  
<img width="584" alt="Screen Shot 2022-08-04 at 09 53 56" src="https://user-images.githubusercontent.com/59098085/182851894-05adcb13-21d3-4705-a243-146f6042122b.png">



### Sorting The Results of Hierarchical Queries

<br/>

#### 📌 C62: Write a query to build the hierarchy from the employees table, including the employee id, last name, salary, the hierarchy path, and the level. The children of each node must be ordered by salary in ascending order, and those with the same salary should be ordered alphabetically by last_name, in descending order.


```sql
select 
    employee_id,
    last_name,
    salary,
    sys_connect_by_path(last_name, '->') as path,
    level
from employees
start with manager_id is null
connect by manager_id = prior employee_id
order siblings by salary, last_name desc;
```

Result:  
<img width="545" alt="Screen Shot 2022-08-04 at 10 18 10" src="https://user-images.githubusercontent.com/59098085/182856681-b22b5eee-2bfe-4f76-b329-719f23b39248.png">


## Additional Practice

<br/>


### Extended practice Schema

<br/>
<details>
<summary>
Click here to see the script for the tables!
</summary>

**To run in ORACLE LIVE I had to devide the query in parts. For some reason ORACLE LIVE does not accepted everything at once.**

```sql
--------------------------------------------------------
--  DDL for Table COUNTRIES
--------------------------------------------------------

  CREATE TABLE "COUNTRIES" ("COUNTRY_ID" CHAR(2), "COUNTRY_NAME" VARCHAR2(40), "REGION_ID" NUMBER,  CONSTRAINT "COUNTRY_C_ID_PK" PRIMARY KEY ("COUNTRY_ID") ENABLE);

   COMMENT ON COLUMN "COUNTRIES"."COUNTRY_ID" IS 'Primary key of countries table.';
   COMMENT ON COLUMN "COUNTRIES"."COUNTRY_NAME" IS 'Country name';
   COMMENT ON COLUMN "COUNTRIES"."REGION_ID" IS 'Region ID for the country. Foreign key to region_id column in the departments table.';
   COMMENT ON TABLE "COUNTRIES"  IS 'country table. Contains 25 rows. References with locations table.';
--------------------------------------------------------
--  DDL for Table DEPARTMENTS
--------------------------------------------------------

  CREATE TABLE "DEPARTMENTS" ("DEPARTMENT_ID" NUMBER(4,0), "DEPARTMENT_NAME" VARCHAR2(30), "MANAGER_ID" NUMBER(6,0), "LOCATION_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "DEPARTMENTS"."DEPARTMENT_ID" IS 'Primary key column of departments table.';
   COMMENT ON COLUMN "DEPARTMENTS"."DEPARTMENT_NAME" IS 'A not null column that shows name of a department. Administration,
Marketing, Purchasing, Human Resources, Shipping, IT, Executive, Public
Relations, Sales, Finance, and Accounting. ';
   COMMENT ON COLUMN "DEPARTMENTS"."MANAGER_ID" IS 'Manager_id of a department. Foreign key to employee_id column of employees table. The manager_id column of the employee table references this column.';
   COMMENT ON COLUMN "DEPARTMENTS"."LOCATION_ID" IS 'Location id where a department is located. Foreign key to location_id column of locations table.';
   COMMENT ON TABLE "DEPARTMENTS"  IS 'Departments table that shows details of departments where employees
work. Contains 27 rows; references with locations, employees, and job_history tables.';
--------------------------------------------------------
--  DDL for Table EMPLOYEES
--------------------------------------------------------

  CREATE TABLE "EMPLOYEES" ("EMPLOYEE_ID" NUMBER(6,0), "FIRST_NAME" VARCHAR2(20), "LAST_NAME" VARCHAR2(25), "EMAIL" VARCHAR2(25), "PHONE_NUMBER" VARCHAR2(20), "HIRE_DATE" DATE, "JOB_ID" VARCHAR2(10), "SALARY" NUMBER(8,2), "COMMISSION_PCT" NUMBER(2,2), "MANAGER_ID" NUMBER(6,0), "DEPARTMENT_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "EMPLOYEES"."EMPLOYEE_ID" IS 'Primary key of employees table.';
   COMMENT ON COLUMN "EMPLOYEES"."FIRST_NAME" IS 'First name of the employee. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."LAST_NAME" IS 'Last name of the employee. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."EMAIL" IS 'Email id of the employee';
   COMMENT ON COLUMN "EMPLOYEES"."PHONE_NUMBER" IS 'Phone number of the employee; includes country code and area code';
   COMMENT ON COLUMN "EMPLOYEES"."HIRE_DATE" IS 'Date when the employee started on this job. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."JOB_ID" IS 'Current job of the employee; foreign key to job_id column of the
jobs table. A not null column.';
   COMMENT ON COLUMN "EMPLOYEES"."SALARY" IS 'Monthly salary of the employee. Must be greater
than zero (enforced by constraint emp_salary_min)';
   COMMENT ON COLUMN "EMPLOYEES"."COMMISSION_PCT" IS 'Commission percentage of the employee; Only employees in sales
department elgible for commission percentage';
   COMMENT ON COLUMN "EMPLOYEES"."MANAGER_ID" IS 'Manager id of the employee; has same domain as manager_id in
departments table. Foreign key to employee_id column of employees table.
(useful for reflexive joins and CONNECT BY query)';
   COMMENT ON COLUMN "EMPLOYEES"."DEPARTMENT_ID" IS 'Department id where employee works; foreign key to department_id
column of the departments table';
   COMMENT ON TABLE "EMPLOYEES"  IS 'employees table. Contains 107 rows. References with departments,
jobs, job_history tables. Contains a self reference.';
--------------------------------------------------------
--  DDL for Table JOB_HISTORY
--------------------------------------------------------

  CREATE TABLE "JOB_HISTORY" ("EMPLOYEE_ID" NUMBER(6,0), "START_DATE" DATE, "END_DATE" DATE, "JOB_ID" VARCHAR2(10), "DEPARTMENT_ID" NUMBER(4,0)) ;

   COMMENT ON COLUMN "JOB_HISTORY"."EMPLOYEE_ID" IS 'A not null column in the complex primary key employee_id+start_date.
Foreign key to employee_id column of the employee table';
   COMMENT ON COLUMN "JOB_HISTORY"."START_DATE" IS 'A not null column in the complex primary key employee_id+start_date.
Must be less than the end_date of the job_history table. (enforced by
constraint jhist_date_interval)';
   COMMENT ON COLUMN "JOB_HISTORY"."END_DATE" IS 'Last day of the employee in this job role. A not null column. Must be
greater than the start_date of the job_history table.
(enforced by constraint jhist_date_interval)';
   COMMENT ON COLUMN "JOB_HISTORY"."JOB_ID" IS 'Job role in which the employee worked in the past; foreign key to
job_id column in the jobs table. A not null column.';
   COMMENT ON COLUMN "JOB_HISTORY"."DEPARTMENT_ID" IS 'Department id in which the employee worked in the past; foreign key to deparment_id column in the departments table';
   COMMENT ON TABLE "JOB_HISTORY"  IS 'Table that stores job history of the employees. If an employee
changes departments within the job or changes jobs within the department,
new rows get inserted into this table with old job information of the
employee. Contains a complex primary key: employee_id+start_date.
Contains 25 rows. References with jobs, employees, and departments tables.';
--------------------------------------------------------
--  DDL for Table JOBS
--------------------------------------------------------

  CREATE TABLE "JOBS" ("JOB_ID" VARCHAR2(10), "JOB_TITLE" VARCHAR2(35), "MIN_SALARY" NUMBER(6,0), "MAX_SALARY" NUMBER(6,0)) ;

   COMMENT ON COLUMN "JOBS"."JOB_ID" IS 'Primary key of jobs table.';
   COMMENT ON COLUMN "JOBS"."JOB_TITLE" IS 'A not null column that shows job title, e.g. AD_VP, FI_ACCOUNTANT';
   COMMENT ON COLUMN "JOBS"."MIN_SALARY" IS 'Minimum salary for a job title.';
   COMMENT ON COLUMN "JOBS"."MAX_SALARY" IS 'Maximum salary for a job title';
   COMMENT ON TABLE "JOBS"  IS 'jobs table with job titles and salary ranges. Contains 19 rows.
References with employees and job_history table.';
--------------------------------------------------------
--  DDL for Table LOCATIONS
--------------------------------------------------------

  CREATE TABLE "LOCATIONS" ("LOCATION_ID" NUMBER(4,0), "STREET_ADDRESS" VARCHAR2(40), "POSTAL_CODE" VARCHAR2(12), "CITY" VARCHAR2(30), "STATE_PROVINCE" VARCHAR2(25), "COUNTRY_ID" CHAR(2)) ;

   COMMENT ON COLUMN "LOCATIONS"."LOCATION_ID" IS 'Primary key of locations table';
   COMMENT ON COLUMN "LOCATIONS"."STREET_ADDRESS" IS 'Street address of an office, warehouse, or production site of a company.
Contains building number and street name';
   COMMENT ON COLUMN "LOCATIONS"."POSTAL_CODE" IS 'Postal code of the location of an office, warehouse, or production site
of a company. ';
   COMMENT ON COLUMN "LOCATIONS"."CITY" IS 'A not null column that shows city where an office, warehouse, or
production site of a company is located. ';
   COMMENT ON COLUMN "LOCATIONS"."STATE_PROVINCE" IS 'State or Province where an office, warehouse, or production site of a
company is located.';
   COMMENT ON COLUMN "LOCATIONS"."COUNTRY_ID" IS 'Country where an office, warehouse, or production site of a company is
located. Foreign key to country_id column of the countries table.';
   COMMENT ON TABLE "LOCATIONS"  IS 'Locations table that contains specific address of a specific office,
warehouse, and/or production site of a company. Does not store addresses /
locations of customers. Contains 23 rows; references with the
departments and countries tables. ';
--------------------------------------------------------
--  DDL for Table REGIONS
--------------------------------------------------------

  CREATE TABLE "REGIONS" ("REGION_ID" NUMBER, "REGION_NAME" VARCHAR2(25));
REM INSERTING into COUNTRIES

Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('AR','Argentina',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('AU','Australia',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('BE','Belgium',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('BR','Brazil',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CA','Canada',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CH','Switzerland',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('CN','China',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('DE','Germany',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('DK','Denmark',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('EG','Egypt',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('FR','France',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IL','Israel',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IN','India',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('IT','Italy',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('JP','Japan',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('KW','Kuwait',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ML','Malaysia',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('MX','Mexico',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('NG','Nigeria',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('NL','Netherlands',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('SG','Singapore',3);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('UK','United Kingdom',1);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('US','United States of America',2);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ZM','Zambia',4);
Insert into COUNTRIES (COUNTRY_ID,COUNTRY_NAME,REGION_ID) values ('ZW','Zimbabwe',4);
REM INSERTING into DEPARTMENTS

Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (10,'Administration',200,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (20,'Marketing',201,1800);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (30,'Purchasing',114,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (40,'Human Resources',203,2400);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (50,'Shipping',121,1500);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (60,'IT',103,1400);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (70,'Public Relations',204,2700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (80,'Sales',145,2500);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (90,'Executive',100,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (100,'Finance',108,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (110,'Accounting',205,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (120,'Treasury',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (130,'Corporate Tax',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (140,'Control And Credit',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (150,'Shareholder Services',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (160,'Benefits',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (170,'Manufacturing',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (180,'Construction',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (190,'Contracting',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (200,'Operations',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (210,'IT Support',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (220,'NOC',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (230,'IT Helpdesk',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (240,'Government Sales',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (250,'Retail Sales',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (260,'Recruiting',null,1700);
Insert into DEPARTMENTS (DEPARTMENT_ID,DEPARTMENT_NAME,MANAGER_ID,LOCATION_ID) values (270,'Payroll',null,1700);
REM INSERTING into EMPLOYEES

Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (100,'Steven','King','SKING','515.123.4567',to_date('17-JUN-03','DD-MON-RR'),'AD_PRES',24000,null,null,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (101,'Neena','Kochhar','NKOCHHAR','515.123.4568',to_date('21-SEP-05','DD-MON-RR'),'AD_VP',17000,null,100,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (102,'Lex','De Haan','LDEHAAN','515.123.4569',to_date('13-JAN-01','DD-MON-RR'),'AD_VP',17000,null,100,90);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (103,'Alexander','Hunold','AHUNOLD','590.423.4567',to_date('03-JAN-06','DD-MON-RR'),'IT_PROG',9000,null,102,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (104,'Bruce','Ernst','BERNST','590.423.4568',to_date('21-MAY-07','DD-MON-RR'),'IT_PROG',6000,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (105,'David','Austin','DAUSTIN','590.423.4569',to_date('25-JUN-05','DD-MON-RR'),'IT_PROG',4800,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (106,'Valli','Pataballa','VPATABAL','590.423.4560',to_date('05-FEB-06','DD-MON-RR'),'IT_PROG',4800,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (107,'Diana','Lorentz','DLORENTZ','590.423.5567',to_date('07-FEB-07','DD-MON-RR'),'IT_PROG',4200,null,103,60);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (108,'Nancy','Greenberg','NGREENBE','515.124.4569',to_date('17-AUG-02','DD-MON-RR'),'FI_MGR',12008,null,101,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (109,'Daniel','Faviet','DFAVIET','515.124.4169',to_date('16-AUG-02','DD-MON-RR'),'FI_ACCOUNT',9000,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (110,'John','Chen','JCHEN','515.124.4269',to_date('28-SEP-05','DD-MON-RR'),'FI_ACCOUNT',8200,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (111,'Ismael','Sciarra','ISCIARRA','515.124.4369',to_date('30-SEP-05','DD-MON-RR'),'FI_ACCOUNT',7700,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (112,'Jose Manuel','Urman','JMURMAN','515.124.4469',to_date('07-MAR-06','DD-MON-RR'),'FI_ACCOUNT',7800,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (113,'Luis','Popp','LPOPP','515.124.4567',to_date('07-DEC-07','DD-MON-RR'),'FI_ACCOUNT',6900,null,108,100);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (114,'Den','Raphaely','DRAPHEAL','515.127.4561',to_date('07-DEC-02','DD-MON-RR'),'PU_MAN',11000,null,100,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (115,'Alexander','Khoo','AKHOO','515.127.4562',to_date('18-MAY-03','DD-MON-RR'),'PU_CLERK',3100,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (116,'Shelli','Baida','SBAIDA','515.127.4563',to_date('24-DEC-05','DD-MON-RR'),'PU_CLERK',2900,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (117,'Sigal','Tobias','STOBIAS','515.127.4564',to_date('24-JUL-05','DD-MON-RR'),'PU_CLERK',2800,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (118,'Guy','Himuro','GHIMURO','515.127.4565',to_date('15-NOV-06','DD-MON-RR'),'PU_CLERK',2600,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (119,'Karen','Colmenares','KCOLMENA','515.127.4566',to_date('10-AUG-07','DD-MON-RR'),'PU_CLERK',2500,null,114,30);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (120,'Matthew','Weiss','MWEISS','650.123.1234',to_date('18-JUL-04','DD-MON-RR'),'ST_MAN',8000,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (121,'Adam','Fripp','AFRIPP','650.123.2234',to_date('10-APR-05','DD-MON-RR'),'ST_MAN',8200,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (122,'Payam','Kaufling','PKAUFLIN','650.123.3234',to_date('01-MAY-03','DD-MON-RR'),'ST_MAN',7900,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (123,'Shanta','Vollman','SVOLLMAN','650.123.4234',to_date('10-OCT-05','DD-MON-RR'),'ST_MAN',6500,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (124,'Kevin','Mourgos','KMOURGOS','650.123.5234',to_date('16-NOV-07','DD-MON-RR'),'ST_MAN',5800,null,100,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (125,'Julia','Nayer','JNAYER','650.124.1214',to_date('16-JUL-05','DD-MON-RR'),'ST_CLERK',3200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (126,'Irene','Mikkilineni','IMIKKILI','650.124.1224',to_date('28-SEP-06','DD-MON-RR'),'ST_CLERK',2700,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (127,'James','Landry','JLANDRY','650.124.1334',to_date('14-JAN-07','DD-MON-RR'),'ST_CLERK',2400,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (128,'Steven','Markle','SMARKLE','650.124.1434',to_date('08-MAR-08','DD-MON-RR'),'ST_CLERK',2200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (129,'Laura','Bissot','LBISSOT','650.124.5234',to_date('20-AUG-05','DD-MON-RR'),'ST_CLERK',3300,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (130,'Mozhe','Atkinson','MATKINSO','650.124.6234',to_date('30-OCT-05','DD-MON-RR'),'ST_CLERK',2800,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (131,'James','Marlow','JAMRLOW','650.124.7234',to_date('16-FEB-05','DD-MON-RR'),'ST_CLERK',2500,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (132,'TJ','Olson','TJOLSON','650.124.8234',to_date('10-APR-07','DD-MON-RR'),'ST_CLERK',2100,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (133,'Jason','Mallin','JMALLIN','650.127.1934',to_date('14-JUN-04','DD-MON-RR'),'ST_CLERK',3300,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (134,'Michael','Rogers','MROGERS','650.127.1834',to_date('26-AUG-06','DD-MON-RR'),'ST_CLERK',2900,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (135,'Ki','Gee','KGEE','650.127.1734',to_date('12-DEC-07','DD-MON-RR'),'ST_CLERK',2400,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (136,'Hazel','Philtanker','HPHILTAN','650.127.1634',to_date('06-FEB-08','DD-MON-RR'),'ST_CLERK',2200,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (137,'Renske','Ladwig','RLADWIG','650.121.1234',to_date('14-JUL-03','DD-MON-RR'),'ST_CLERK',3600,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (138,'Stephen','Stiles','SSTILES','650.121.2034',to_date('26-OCT-05','DD-MON-RR'),'ST_CLERK',3200,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (139,'John','Seo','JSEO','650.121.2019',to_date('12-FEB-06','DD-MON-RR'),'ST_CLERK',2700,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (140,'Joshua','Patel','JPATEL','650.121.1834',to_date('06-APR-06','DD-MON-RR'),'ST_CLERK',2500,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (141,'Trenna','Rajs','TRAJS','650.121.8009',to_date('17-OCT-03','DD-MON-RR'),'ST_CLERK',3500,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (142,'Curtis','Davies','CDAVIES','650.121.2994',to_date('29-JAN-05','DD-MON-RR'),'ST_CLERK',3100,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (143,'Randall','Matos','RMATOS','650.121.2874',to_date('15-MAR-06','DD-MON-RR'),'ST_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (144,'Peter','Vargas','PVARGAS','650.121.2004',to_date('09-JUL-06','DD-MON-RR'),'ST_CLERK',2500,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (145,'John','Russell','JRUSSEL','011.44.1344.429268',to_date('01-OCT-04','DD-MON-RR'),'SA_MAN',14000,0.4,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (146,'Karen','Partners','KPARTNER','011.44.1344.467268',to_date('05-JAN-05','DD-MON-RR'),'SA_MAN',13500,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (147,'Alberto','Errazuriz','AERRAZUR','011.44.1344.429278',to_date('10-MAR-05','DD-MON-RR'),'SA_MAN',12000,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (148,'Gerald','Cambrault','GCAMBRAU','011.44.1344.619268',to_date('15-OCT-07','DD-MON-RR'),'SA_MAN',11000,0.3,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (149,'Eleni','Zlotkey','EZLOTKEY','011.44.1344.429018',to_date('29-JAN-08','DD-MON-RR'),'SA_MAN',10500,0.2,100,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (150,'Peter','Tucker','PTUCKER','011.44.1344.129268',to_date('30-JAN-05','DD-MON-RR'),'SA_REP',10000,0.3,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (151,'David','Bernstein','DBERNSTE','011.44.1344.345268',to_date('24-MAR-05','DD-MON-RR'),'SA_REP',9500,0.25,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (152,'Peter','Hall','PHALL','011.44.1344.478968',to_date('20-AUG-05','DD-MON-RR'),'SA_REP',9000,0.25,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (153,'Christopher','Olsen','COLSEN','011.44.1344.498718',to_date('30-MAR-06','DD-MON-RR'),'SA_REP',8000,0.2,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (154,'Nanette','Cambrault','NCAMBRAU','011.44.1344.987668',to_date('09-DEC-06','DD-MON-RR'),'SA_REP',7500,0.2,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (155,'Oliver','Tuvault','OTUVAULT','011.44.1344.486508',to_date('23-NOV-07','DD-MON-RR'),'SA_REP',7000,0.15,145,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (156,'Janette','King','JKING','011.44.1345.429268',to_date('30-JAN-04','DD-MON-RR'),'SA_REP',10000,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (157,'Patrick','Sully','PSULLY','011.44.1345.929268',to_date('04-MAR-04','DD-MON-RR'),'SA_REP',9500,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (158,'Allan','McEwen','AMCEWEN','011.44.1345.829268',to_date('01-AUG-04','DD-MON-RR'),'SA_REP',9000,0.35,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (159,'Lindsey','Smith','LSMITH','011.44.1345.729268',to_date('10-MAR-05','DD-MON-RR'),'SA_REP',8000,0.3,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (160,'Louise','Doran','LDORAN','011.44.1345.629268',to_date('15-DEC-05','DD-MON-RR'),'SA_REP',7500,0.3,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (161,'Sarath','Sewall','SSEWALL','011.44.1345.529268',to_date('03-NOV-06','DD-MON-RR'),'SA_REP',7000,0.25,146,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (162,'Clara','Vishney','CVISHNEY','011.44.1346.129268',to_date('11-NOV-05','DD-MON-RR'),'SA_REP',10500,0.25,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (163,'Danielle','Greene','DGREENE','011.44.1346.229268',to_date('19-MAR-07','DD-MON-RR'),'SA_REP',9500,0.15,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (164,'Mattea','Marvins','MMARVINS','011.44.1346.329268',to_date('24-JAN-08','DD-MON-RR'),'SA_REP',7200,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (165,'David','Lee','DLEE','011.44.1346.529268',to_date('23-FEB-08','DD-MON-RR'),'SA_REP',6800,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (166,'Sundar','Ande','SANDE','011.44.1346.629268',to_date('24-MAR-08','DD-MON-RR'),'SA_REP',6400,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (167,'Amit','Banda','ABANDA','011.44.1346.729268',to_date('21-APR-08','DD-MON-RR'),'SA_REP',6200,0.1,147,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (168,'Lisa','Ozer','LOZER','011.44.1343.929268',to_date('11-MAR-05','DD-MON-RR'),'SA_REP',11500,0.25,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (169,'Harrison','Bloom','HBLOOM','011.44.1343.829268',to_date('23-MAR-06','DD-MON-RR'),'SA_REP',10000,0.2,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (170,'Tayler','Fox','TFOX','011.44.1343.729268',to_date('24-JAN-06','DD-MON-RR'),'SA_REP',9600,0.2,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (171,'William','Smith','WSMITH','011.44.1343.629268',to_date('23-FEB-07','DD-MON-RR'),'SA_REP',7400,0.15,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (172,'Elizabeth','Bates','EBATES','011.44.1343.529268',to_date('24-MAR-07','DD-MON-RR'),'SA_REP',7300,0.15,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (173,'Sundita','Kumar','SKUMAR','011.44.1343.329268',to_date('21-APR-08','DD-MON-RR'),'SA_REP',6100,0.1,148,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (174,'Ellen','Abel','EABEL','011.44.1644.429267',to_date('11-MAY-04','DD-MON-RR'),'SA_REP',11000,0.3,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (175,'Alyssa','Hutton','AHUTTON','011.44.1644.429266',to_date('19-MAR-05','DD-MON-RR'),'SA_REP',8800,0.25,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (176,'Jonathon','Taylor','JTAYLOR','011.44.1644.429265',to_date('24-MAR-06','DD-MON-RR'),'SA_REP',8600,0.2,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (177,'Jack','Livingston','JLIVINGS','011.44.1644.429264',to_date('23-APR-06','DD-MON-RR'),'SA_REP',8400,0.2,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (178,'Kimberely','Grant','KGRANT','011.44.1644.429263',to_date('24-MAY-07','DD-MON-RR'),'SA_REP',7000,0.15,149,null);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (179,'Charles','Johnson','CJOHNSON','011.44.1644.429262',to_date('04-JAN-08','DD-MON-RR'),'SA_REP',6200,0.1,149,80);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (180,'Winston','Taylor','WTAYLOR','650.507.9876',to_date('24-JAN-06','DD-MON-RR'),'SH_CLERK',3200,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (181,'Jean','Fleaur','JFLEAUR','650.507.9877',to_date('23-FEB-06','DD-MON-RR'),'SH_CLERK',3100,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (182,'Martha','Sullivan','MSULLIVA','650.507.9878',to_date('21-JUN-07','DD-MON-RR'),'SH_CLERK',2500,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (183,'Girard','Geoni','GGEONI','650.507.9879',to_date('03-FEB-08','DD-MON-RR'),'SH_CLERK',2800,null,120,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (184,'Nandita','Sarchand','NSARCHAN','650.509.1876',to_date('27-JAN-04','DD-MON-RR'),'SH_CLERK',4200,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (185,'Alexis','Bull','ABULL','650.509.2876',to_date('20-FEB-05','DD-MON-RR'),'SH_CLERK',4100,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (186,'Julia','Dellinger','JDELLING','650.509.3876',to_date('24-JUN-06','DD-MON-RR'),'SH_CLERK',3400,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (187,'Anthony','Cabrio','ACABRIO','650.509.4876',to_date('07-FEB-07','DD-MON-RR'),'SH_CLERK',3000,null,121,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (188,'Kelly','Chung','KCHUNG','650.505.1876',to_date('14-JUN-05','DD-MON-RR'),'SH_CLERK',3800,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (189,'Jennifer','Dilly','JDILLY','650.505.2876',to_date('13-AUG-05','DD-MON-RR'),'SH_CLERK',3600,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (190,'Timothy','Gates','TGATES','650.505.3876',to_date('11-JUL-06','DD-MON-RR'),'SH_CLERK',2900,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (191,'Randall','Perkins','RPERKINS','650.505.4876',to_date('19-DEC-07','DD-MON-RR'),'SH_CLERK',2500,null,122,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (192,'Sarah','Bell','SBELL','650.501.1876',to_date('04-FEB-04','DD-MON-RR'),'SH_CLERK',4000,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (193,'Britney','Everett','BEVERETT','650.501.2876',to_date('03-MAR-05','DD-MON-RR'),'SH_CLERK',3900,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (194,'Samuel','McCain','SMCCAIN','650.501.3876',to_date('01-JUL-06','DD-MON-RR'),'SH_CLERK',3200,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (195,'Vance','Jones','VJONES','650.501.4876',to_date('17-MAR-07','DD-MON-RR'),'SH_CLERK',2800,null,123,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (196,'Alana','Walsh','AWALSH','650.507.9811',to_date('24-APR-06','DD-MON-RR'),'SH_CLERK',3100,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (197,'Kevin','Feeney','KFEENEY','650.507.9822',to_date('23-MAY-06','DD-MON-RR'),'SH_CLERK',3000,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (198,'Donald','OConnell','DOCONNEL','650.507.9833',to_date('21-JUN-07','DD-MON-RR'),'SH_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (199,'Douglas','Grant','DGRANT','650.507.9844',to_date('13-JAN-08','DD-MON-RR'),'SH_CLERK',2600,null,124,50);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (200,'Jennifer','Whalen','JWHALEN','515.123.4444',to_date('17-SEP-03','DD-MON-RR'),'AD_ASST',4400,null,101,10);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (201,'Michael','Hartstein','MHARTSTE','515.123.5555',to_date('17-FEB-04','DD-MON-RR'),'MK_MAN',13000,null,100,20);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (202,'Pat','Fay','PFAY','603.123.6666',to_date('17-AUG-05','DD-MON-RR'),'MK_REP',6000,null,201,20);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (203,'Susan','Mavris','SMAVRIS','515.123.7777',to_date('07-JUN-02','DD-MON-RR'),'HR_REP',6500,null,101,40);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (204,'Hermann','Baer','HBAER','515.123.8888',to_date('07-JUN-02','DD-MON-RR'),'PR_REP',10000,null,101,70);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (205,'Shelley','Higgins','SHIGGINS','515.123.8080',to_date('07-JUN-02','DD-MON-RR'),'AC_MGR',12008,null,101,110);
Insert into EMPLOYEES (EMPLOYEE_ID,FIRST_NAME,LAST_NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,JOB_ID,SALARY,COMMISSION_PCT,MANAGER_ID,DEPARTMENT_ID) values (206,'William','Gietz','WGIETZ','515.123.8181',to_date('07-JUN-02','DD-MON-RR'),'AC_ACCOUNT',8300,null,205,110);
REM INSERTING into JOB_HISTORY

Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (102,to_date('13-JAN-01','DD-MON-RR'),to_date('24-JUL-06','DD-MON-RR'),'IT_PROG',60);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (101,to_date('21-SEP-97','DD-MON-RR'),to_date('27-OCT-01','DD-MON-RR'),'AC_ACCOUNT',110);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (101,to_date('28-OCT-01','DD-MON-RR'),to_date('15-MAR-05','DD-MON-RR'),'AC_MGR',110);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (201,to_date('17-FEB-04','DD-MON-RR'),to_date('19-DEC-07','DD-MON-RR'),'MK_REP',20);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (114,to_date('24-MAR-06','DD-MON-RR'),to_date('31-DEC-07','DD-MON-RR'),'ST_CLERK',50);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (122,to_date('01-JAN-07','DD-MON-RR'),to_date('31-DEC-07','DD-MON-RR'),'ST_CLERK',50);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (200,to_date('17-SEP-95','DD-MON-RR'),to_date('17-JUN-01','DD-MON-RR'),'AD_ASST',90);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (176,to_date('24-MAR-06','DD-MON-RR'),to_date('31-DEC-06','DD-MON-RR'),'SA_REP',80);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (176,to_date('01-JAN-07','DD-MON-RR'),to_date('31-DEC-07','DD-MON-RR'),'SA_MAN',80);
Insert into JOB_HISTORY (EMPLOYEE_ID,START_DATE,END_DATE,JOB_ID,DEPARTMENT_ID) values (200,to_date('01-JUL-02','DD-MON-RR'),to_date('31-DEC-06','DD-MON-RR'),'AC_ACCOUNT',90);
REM INSERTING into JOBS

Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_PRES','President',20080,40000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_VP','Administration Vice President',15000,30000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AD_ASST','Administration Assistant',3000,6000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('FI_MGR','Finance Manager',8200,16000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('FI_ACCOUNT','Accountant',4200,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AC_MGR','Accounting Manager',8200,16000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('AC_ACCOUNT','Public Accountant',4200,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SA_MAN','Sales Manager',10000,20080);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SA_REP','Sales Representative',6000,12008);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PU_MAN','Purchasing Manager',8000,15000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PU_CLERK','Purchasing Clerk',2500,5500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('ST_MAN','Stock Manager',5500,8500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('ST_CLERK','Stock Clerk',2008,5000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('SH_CLERK','Shipping Clerk',2500,5500);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('IT_PROG','Programmer',4000,10000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('MK_MAN','Marketing Manager',9000,15000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('MK_REP','Marketing Representative',4000,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('HR_REP','Human Resources Representative',4000,9000);
Insert into JOBS (JOB_ID,JOB_TITLE,MIN_SALARY,MAX_SALARY) values ('PR_REP','Public Relations Representative',4500,10500);
REM INSERTING into LOCATIONS

Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1000,'1297 Via Cola di Rie','00989','Roma',null,'IT');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1100,'93091 Calle della Testa','10934','Venice',null,'IT');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1200,'2017 Shinjuku-ku','1689','Tokyo','Tokyo Prefecture','JP');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1300,'9450 Kamiya-cho','6823','Hiroshima',null,'JP');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1400,'2014 Jabberwocky Rd','26192','Southlake','Texas','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1500,'2011 Interiors Blvd','99236','South San Francisco','California','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1600,'2007 Zagora St','50090','South Brunswick','New Jersey','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1700,'2004 Charade Rd','98199','Seattle','Washington','US');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1800,'147 Spadina Ave','M5V 2L7','Toronto','Ontario','CA');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (1900,'6092 Boxwood St','YSW 9T2','Whitehorse','Yukon','CA');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2000,'40-5-12 Laogianggen','190518','Beijing',null,'CN');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2100,'1298 Vileparle (E)','490231','Bombay','Maharashtra','IN');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2200,'12-98 Victoria Street','2901','Sydney','New South Wales','AU');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2300,'198 Clementi North','540198','Singapore',null,'SG');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2400,'8204 Arthur St',null,'London',null,'UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2500,'Magdalen Centre, The Oxford Science Park','OX9 9ZB','Oxford','Oxford','UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2600,'9702 Chester Road','09629850293','Stretford','Manchester','UK');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2700,'Schwanthalerstr. 7031','80925','Munich','Bavaria','DE');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2800,'Rua Frei Caneca 1360 ','01307-002','Sao Paulo','Sao Paulo','BR');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (2900,'20 Rue des Corps-Saints','1730','Geneva','Geneve','CH');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3000,'Murtenstrasse 921','3095','Bern','BE','CH');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3100,'Pieter Breughelstraat 837','3029SK','Utrecht','Utrecht','NL');
Insert into LOCATIONS (LOCATION_ID,STREET_ADDRESS,POSTAL_CODE,CITY,STATE_PROVINCE,COUNTRY_ID) values (3200,'Mariano Escobedo 9991','11932','Mexico City','Distrito Federal,','MX');
REM INSERTING into REGIONS

Insert into REGIONS (REGION_ID,REGION_NAME) values (1,'Europe');
Insert into REGIONS (REGION_ID,REGION_NAME) values (2,'Americas');
Insert into REGIONS (REGION_ID,REGION_NAME) values (3,'Asia');
Insert into REGIONS (REGION_ID,REGION_NAME) values (4,'Middle East and Africa');
--------------------------------------------------------
--  DDL for Index DEPT_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "DEPT_ID_PK" ON "DEPARTMENTS" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index DEPT_LOCATION_IX
--------------------------------------------------------

  CREATE INDEX "DEPT_LOCATION_IX" ON "DEPARTMENTS" ("LOCATION_ID");
--------------------------------------------------------
--  DDL for Index EMP_EMAIL_UK
--------------------------------------------------------

  CREATE UNIQUE INDEX "EMP_EMAIL_UK" ON "EMPLOYEES" ("EMAIL");
--------------------------------------------------------
--  DDL for Index EMP_EMP_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "EMP_EMP_ID_PK" ON "EMPLOYEES" ("EMPLOYEE_ID");
--------------------------------------------------------
--  DDL for Index EMP_DEPARTMENT_IX
--------------------------------------------------------

  CREATE INDEX "EMP_DEPARTMENT_IX" ON "EMPLOYEES" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index EMP_JOB_IX
--------------------------------------------------------

  CREATE INDEX "EMP_JOB_IX" ON "EMPLOYEES" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index EMP_MANAGER_IX
--------------------------------------------------------

  CREATE INDEX "EMP_MANAGER_IX" ON "EMPLOYEES" ("MANAGER_ID");
--------------------------------------------------------
--  DDL for Index EMP_NAME_IX
--------------------------------------------------------

  CREATE INDEX "EMP_NAME_IX" ON "EMPLOYEES" ("LAST_NAME", "FIRST_NAME");
--------------------------------------------------------
--  DDL for Index JHIST_EMP_ID_ST_DATE_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "JHIST_EMP_ID_ST_DATE_PK" ON "JOB_HISTORY" ("EMPLOYEE_ID", "START_DATE");
--------------------------------------------------------
--  DDL for Index JHIST_JOB_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_JOB_IX" ON "JOB_HISTORY" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index JHIST_EMPLOYEE_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_EMPLOYEE_IX" ON "JOB_HISTORY" ("EMPLOYEE_ID");
--------------------------------------------------------
--  DDL for Index JHIST_DEPARTMENT_IX
--------------------------------------------------------

  CREATE INDEX "JHIST_DEPARTMENT_IX" ON "JOB_HISTORY" ("DEPARTMENT_ID");
--------------------------------------------------------
--  DDL for Index JOB_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "JOB_ID_PK" ON "JOBS" ("JOB_ID");
--------------------------------------------------------
--  DDL for Index LOC_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "LOC_ID_PK" ON "LOCATIONS" ("LOCATION_ID");
--------------------------------------------------------
--  DDL for Index LOC_CITY_IX
--------------------------------------------------------

  CREATE INDEX "LOC_CITY_IX" ON "LOCATIONS" ("CITY");
--------------------------------------------------------
--  DDL for Index LOC_STATE_PROVINCE_IX
--------------------------------------------------------

  CREATE INDEX "LOC_STATE_PROVINCE_IX" ON "LOCATIONS" ("STATE_PROVINCE");
--------------------------------------------------------
--  DDL for Index LOC_COUNTRY_IX
--------------------------------------------------------

  CREATE INDEX "LOC_COUNTRY_IX" ON "LOCATIONS" ("COUNTRY_ID");
--------------------------------------------------------
--  DDL for Index REG_ID_PK
--------------------------------------------------------

  CREATE UNIQUE INDEX "REG_ID_PK" ON "REGIONS" ("REGION_ID");
--------------------------------------------------------
--  Constraints for Table COUNTRIES
--------------------------------------------------------

  ALTER TABLE "COUNTRIES" MODIFY ("COUNTRY_ID" CONSTRAINT "COUNTRY_ID_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table DEPARTMENTS
--------------------------------------------------------

  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_ID_PK" PRIMARY KEY ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "DEPARTMENTS" MODIFY ("DEPARTMENT_NAME" CONSTRAINT "DEPT_NAME_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table EMPLOYEES
--------------------------------------------------------

  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_EMP_ID_PK" PRIMARY KEY ("EMPLOYEE_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_EMAIL_UK" UNIQUE ("EMAIL") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_SALARY_MIN" CHECK (salary > 0) ENABLE;
  ALTER TABLE "EMPLOYEES" MODIFY ("JOB_ID" CONSTRAINT "EMP_JOB_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("HIRE_DATE" CONSTRAINT "EMP_HIRE_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("EMAIL" CONSTRAINT "EMP_EMAIL_NN" NOT NULL ENABLE);
  ALTER TABLE "EMPLOYEES" MODIFY ("LAST_NAME" CONSTRAINT "EMP_LAST_NAME_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table JOB_HISTORY
--------------------------------------------------------

  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_EMP_ID_ST_DATE_PK" PRIMARY KEY ("EMPLOYEE_ID", "START_DATE") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_DATE_INTERVAL" CHECK (end_date > start_date) ENABLE;
  ALTER TABLE "JOB_HISTORY" MODIFY ("JOB_ID" CONSTRAINT "JHIST_JOB_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("END_DATE" CONSTRAINT "JHIST_END_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("START_DATE" CONSTRAINT "JHIST_START_DATE_NN" NOT NULL ENABLE);
  ALTER TABLE "JOB_HISTORY" MODIFY ("EMPLOYEE_ID" CONSTRAINT "JHIST_EMPLOYEE_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table JOBS
--------------------------------------------------------

  ALTER TABLE "JOBS" ADD CONSTRAINT "JOB_ID_PK" PRIMARY KEY ("JOB_ID") ENABLE;
  ALTER TABLE "JOBS" MODIFY ("JOB_TITLE" CONSTRAINT "JOB_TITLE_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table LOCATIONS
--------------------------------------------------------

  ALTER TABLE "LOCATIONS" ADD CONSTRAINT "LOC_ID_PK" PRIMARY KEY ("LOCATION_ID") ENABLE;
  ALTER TABLE "LOCATIONS" MODIFY ("CITY" CONSTRAINT "LOC_CITY_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Constraints for Table REGIONS
--------------------------------------------------------

  ALTER TABLE "REGIONS" ADD CONSTRAINT "REG_ID_PK" PRIMARY KEY ("REGION_ID") ENABLE;
  ALTER TABLE "REGIONS" MODIFY ("REGION_ID" CONSTRAINT "REGION_ID_NN" NOT NULL ENABLE);
--------------------------------------------------------
--  Ref Constraints for Table COUNTRIES
--------------------------------------------------------

  ALTER TABLE "COUNTRIES" ADD CONSTRAINT "COUNTR_REG_FK" FOREIGN KEY ("REGION_ID") REFERENCES "REGIONS" ("REGION_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table DEPARTMENTS
--------------------------------------------------------

  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_LOC_FK" FOREIGN KEY ("LOCATION_ID") REFERENCES "LOCATIONS" ("LOCATION_ID") ENABLE;
  ALTER TABLE "DEPARTMENTS" ADD CONSTRAINT "DEPT_MGR_FK" FOREIGN KEY ("MANAGER_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table EMPLOYEES
--------------------------------------------------------

  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_DEPT_FK" FOREIGN KEY ("DEPARTMENT_ID") REFERENCES "DEPARTMENTS" ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_JOB_FK" FOREIGN KEY ("JOB_ID") REFERENCES "JOBS" ("JOB_ID") ENABLE;
  ALTER TABLE "EMPLOYEES" ADD CONSTRAINT "EMP_MANAGER_FK" FOREIGN KEY ("MANAGER_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table JOB_HISTORY
--------------------------------------------------------

  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_DEPT_FK" FOREIGN KEY ("DEPARTMENT_ID") REFERENCES "DEPARTMENTS" ("DEPARTMENT_ID") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_EMP_FK" FOREIGN KEY ("EMPLOYEE_ID") REFERENCES "EMPLOYEES" ("EMPLOYEE_ID") ENABLE;
  ALTER TABLE "JOB_HISTORY" ADD CONSTRAINT "JHIST_JOB_FK" FOREIGN KEY ("JOB_ID") REFERENCES "JOBS" ("JOB_ID") ENABLE;
--------------------------------------------------------
--  Ref Constraints for Table LOCATIONS
--------------------------------------------------------

  ALTER TABLE "LOCATIONS" ADD CONSTRAINT "LOC_C_ID_FK" FOREIGN KEY ("COUNTRY_ID") REFERENCES "COUNTRIES" ("COUNTRY_ID") ENABLE;


--***

REM Extending the schema with additional tables

--======
  --DDL
--======

CREATE TABLE users
  (
    user_id VARCHAR2(10) CONSTRAINT pk_users PRIMARY KEY,
    employee_id NUMBER(6) NOT NULL CONSTRAINT fk_users_employees REFERENCES employees,
    active VARCHAR2(1) NOT NULL,
    creation_date DATE NOT NULL
  );

CREATE TABLE roles
  (
    role_id NUMBER(3) CONSTRAINT pk_roles PRIMARY KEY,
    role_name VARCHAR2(50)
  );

CREATE TABLE user_roles
  (
    user_id VARCHAR2(10) CONSTRAINT fk_userroles_users REFERENCES users,
    role_id NUMBER(3) CONSTRAINT fk_userroles_roles REFERENCES ROLES,
    CONSTRAINT pk_user_roles PRIMARY KEY (user_id,role_id)
  );  

CREATE TABLE systems
  (
    system_id NUMBER(3) CONSTRAINT pk_systems PRIMARY KEY,
    system_name VARCHAR2(50)
  );

CREATE TABLE applications
  (
    application_id NUMBER(5) CONSTRAINT pk_applications PRIMARY KEY,
    application_name VARCHAR2(50),
    system_id NUMBER(3) CONSTRAINT fk_applications_systems REFERENCES systems
  );

CREATE TABLE application_permissions
  (
    application_id NUMBER(5) CONSTRAINT fk_apppermissions_apps REFERENCES applications,
    role_id NUMBER(3) CONSTRAINT fk_apppermissions_roles REFERENCES roles,
    CONSTRAINT pk_application_permissions PRIMARY KEY (application_id,role_id)
  ); 

--======
  --Data
--======

REM Inserting data into the new tables

--Users
INSERT INTO users
SELECT SUBSTR(REPLACE(upper(last_name),' '),1,3) || employee_id,employee_id,
  CASE
    WHEN mod(employee_id,2) = 0
    THEN 'Y'
    ELSE 'N'
  END,hire_date + 10
FROM employees;

--ROLES
INSERT INTO ROLES VALUES (1,'BASIC USER');
INSERT INTO ROLES VALUES (2,'MARKETING FULL');
INSERT INTO ROLES VALUES (3,'PURCHASING QUERY-ONLY');
INSERT INTO ROLES VALUES (4,'PURCHASING FULL');
INSERT INTO ROLES VALUES (5,'HUMAN RESOURCES FULL');
INSERT INTO ROLES VALUES (6,'SHIPPING LEVEL 1');
INSERT INTO ROLES VALUES (7,'SHIPPING LEVEL 2');
INSERT INTO ROLES VALUES (8,'SHIPPING STOCK');
INSERT INTO ROLES VALUES (9,'SHIPPING FULL');
INSERT INTO ROLES VALUES (10,'IT PROGRAMMER QUERY-ONLY');
INSERT INTO ROLES VALUES (11,'IT PROGRAMMER FULL');
INSERT INTO ROLES VALUES (12,'SALES LOCAL');
INSERT INTO ROLES VALUES (13,'SALES REGIONAL');
INSERT INTO ROLES VALUES (14,'FINANCE LEVEL 1');
INSERT INTO ROLES VALUES (15,'FINANCE FULL');
INSERT INTO ROLES VALUES (16,'ACCOUNTING');

--USER_ROLES
INSERT
INTO user_roles
	SELECT user_id, 1
	FROM users;
	
INSERT
INTO user_roles
   SELECT user_id, 2
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 20;
   
INSERT
INTO user_roles
   SELECT user_id, decode(e.job_id,'PU_CLERK',3,4)
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 30;   

INSERT
INTO user_roles
   SELECT user_id, 5
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 40; 

INSERT
INTO user_roles
   SELECT user_id,
      CASE 
         WHEN job_id = 'SH_CLERK' and MOD(e.employee_id,2) = 0
            THEN 6
         WHEN job_id = 'SH_CLERK'
            THEN 7
         WHEN job_id = 'ST_CLERK'
            THEN 8
         ELSE 9
      END
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 50;  

INSERT
INTO user_roles
   SELECT user_id, decode(mod(e.employee_id,2),0,10,11)
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 60;

INSERT
INTO user_roles
   SELECT user_id, decode(mod(e.employee_id,2),0,12,13)
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 80;

INSERT
INTO user_roles
   SELECT user_id, decode(e.job_id,'FI_ACCOUNT',14,15)
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 100;

INSERT
INTO user_roles
   SELECT user_id, 16
   FROM users u
      JOIN employees e
      ON u.employee_id = e.employee_id
   WHERE department_id = 110
      AND job_id = 'AC_MGR';

--SYSTEMS
INSERT INTO systems VALUES (1,'SALES AND MARKETING');
INSERT INTO systems VALUES (2,'CUSTOMER RELATIONSHIP MANAGEMENT');
INSERT INTO systems VALUES (3,'PURCHASING');
INSERT INTO systems VALUES (4,'HUMAN RESOURCES MANAGEMENT');
INSERT INTO systems VALUES (5,'DISTRIBUTION');
INSERT INTO systems VALUES (6,'IT SERVICE MANAGEMENT');
INSERT INTO systems VALUES (7,'FINANCE AND ACCOUNTING');

--APPLICATIONS
INSERT INTO applications VALUES (1,'SALES PLANNING',1);
INSERT INTO applications VALUES (2,'SALES BI',1);
INSERT INTO applications VALUES (3,'CAMPAIGN PLANNING',1);
INSERT INTO applications VALUES (4,'SALES LIVE REPORT',1);
INSERT INTO applications VALUES (5,'ACCOUNT ASSIGNMENT',1);
INSERT INTO applications VALUES (6,'AGENT PERFORMANCE ANALYSIS',1);
INSERT INTO applications VALUES (7,'CUSTOMER BASIC QUERY',2);
INSERT INTO applications VALUES (8,'CUSTOMER RECORD MAINTENANCE',2);
INSERT INTO applications VALUES (9,'SUPPORT CASE MANAGEMENT',2);
INSERT INTO applications VALUES (10,'CUSTOMER BEHAVIOR ANALYSIS',2);
INSERT INTO applications VALUES (11,'INCENTIVE PROGRAM MANAGEMENT',2);
INSERT INTO applications VALUES (12,'QUOTE MANAGEMENT',3);
INSERT INTO applications VALUES (13,'AGREEMENT MANAGEMENT',3);
INSERT INTO applications VALUES (14,'PURCHASING BI',3);
INSERT INTO applications VALUES (15,'PROVIDER ANALYSIS',3);
INSERT INTO applications VALUES (16,'PURCHASE PRE-FILTER',3);
INSERT INTO applications VALUES (17,'PURCHASE PROCESSING',3);
INSERT INTO applications VALUES (18,'RECRUITMENT AND SELECTION',4);
INSERT INTO applications VALUES (19,'EMPLOYEE RECORD MANAGEMENT',4);
INSERT INTO applications VALUES (20,'CAREER ANALYSIS',4);
INSERT INTO applications VALUES (21,'PAYROLL PARAMETERS MANAGEMENT',4);
INSERT INTO applications VALUES (22,'INTERNAL COMMUNICATIONS MANAGEMENT',4);
INSERT INTO applications VALUES (23,'HUMAN RESOURCES BI',4);
INSERT INTO applications VALUES (24,'DISTRIBUTION PLANNING',5);
INSERT INTO applications VALUES (25,'DISTRIBUTION PERFORMANCE ANALYSIS',5);
INSERT INTO applications VALUES (26,'DELIVERY REGISTRATION',5);
INSERT INTO applications VALUES (27,'DELIVERY CASE MANAGEMENT',5);
INSERT INTO applications VALUES (28,'CHANNEL AND PARTNER MANAGEMENT',5);
INSERT INTO applications VALUES (29,'CMDB MAINTENANCE',6);
INSERT INTO applications VALUES (30,'SUPPORT CASE MANAGEMENT',6);
INSERT INTO applications VALUES (31,'CENTRAL MONITORING CONSOLE',6);
INSERT INTO applications VALUES (32,'GENERAL STATUS REPORT',6);
INSERT INTO applications VALUES (33,'FINANCE PLANNING',7);
INSERT INTO applications VALUES (34,'BUDGET MANAGEMENT',7);
INSERT INTO applications VALUES (35,'INVENTORY MANAGEMENT',7);
INSERT INTO applications VALUES (36,'CREDITOR MANAGEMENT',7);
INSERT INTO applications VALUES (37,'ACCOUNTS PAYABLE',7);
INSERT INTO applications VALUES (38,'ACCOUNTS RECEIVABLE',7);
INSERT INTO applications VALUES (39,'ASSET MANAGEMENT',7);
INSERT INTO applications VALUES (40,'AUDIT REGISTRATION',7);

--APPLICATION_PERMISSIONS
INSERT INTO application_permissions
   SELECT application_id,1
   FROM applications
   WHERE application_id in (4,7,22,32);
   
INSERT INTO application_permissions
   SELECT application_id,2
   FROM applications
   WHERE application_id in (1,3,5);   

INSERT INTO application_permissions
   SELECT application_id,3
   FROM applications
   WHERE application_id in (14,15); 

INSERT INTO application_permissions
   SELECT application_id,4
   FROM applications
   WHERE system_id = 3;   
   
INSERT INTO application_permissions
   SELECT application_id,5
   FROM applications
   WHERE system_id = 4;  

INSERT INTO application_permissions
   SELECT application_id,6
   FROM applications
   WHERE application_id in (26); 

INSERT INTO application_permissions
   SELECT application_id,7
   FROM applications
   WHERE application_id in (26,27);    
   
INSERT INTO application_permissions
   SELECT application_id,8
   FROM applications
   WHERE application_id in (24); 

INSERT INTO application_permissions
   SELECT application_id,9
   FROM applications
   WHERE system_id = 5;

INSERT INTO application_permissions
   SELECT application_id,10
   FROM applications
   WHERE application_id in (31,32); 

INSERT INTO application_permissions
   SELECT application_id,11
   FROM applications
   WHERE system_id = 6; 

INSERT INTO application_permissions
   SELECT application_id,12
   FROM applications
   WHERE application_id in (4,5,6); 

INSERT INTO application_permissions
   SELECT application_id,13
   FROM applications
   WHERE system_id = 1;

INSERT INTO application_permissions
   SELECT application_id,14
   FROM applications
   WHERE application_id in (35,36,37,38); 

INSERT INTO application_permissions
   SELECT application_id,15
   FROM applications
   WHERE system_id = 7;

INSERT INTO application_permissions
   SELECT application_id,16
   FROM applications
   WHERE application_id in (37,38,39); 

COMMIT;

CREATE OR REPLACE VIEW v_active_user_count AS
SELECT *
FROM
  (
    SELECT u.active,d.department_name
    FROM users u
    JOIN employees e
    ON u.employee_id = e.employee_id
    JOIN departments d
    ON e.department_id = d.department_id
  )
pivot
(count(*) FOR department_name IN 
('Executive' AS executive,
  'IT' AS it,
  'Finance' AS finance,
  'Purchasing' AS purchasing,
  'Shipping' AS shipping,
  'Sales' AS sales,
  'Administration' AS administration,
  'Marketing' AS marketing,
  'Human Resources' AS human_resources,
  'Public Relations' AS public_relations,
  'Accounting' AS accounting)
);
```

</details>

<br/>

#### 📌 C63: Write a query to generate a list of employees applying the following conditions:    

<strong>

- The results include the employee_id, first_name and last_name columns, but the column titles must use blank spaces to separate words, instead of underscores.

- The salary is less than 3000.

- The first or last names start with ‘G’.
</strong>


```sql
select
        employee_id as "employee id",
        first_name as "first name",
        last_name as "last name"
from employees
where salary < 3000 
and (first_name like 'G%' or last_name like 'G%');
```

Result:  
<img width="264" alt="Screen Shot 2022-08-04 at 21 48 38" src="https://user-images.githubusercontent.com/59098085/182978672-33e11aa2-eb6f-498b-9858-7c2dd0f01e38.png">



#### 📌 C64: Write a query to generate a list of employees who are managers of more than 6 employees, applying the following conditions:        

<strong>

- The results include only the employee_id and the number of employees for whom he/she is the manager.

- The results must be ordered by employee id in descending order.

- Even though you will use the manager_id column in your query, the results must display it as employee_id.
</strong>


```sql
select 
    sup.employee_id,
    count(sub.employee_id) as number_of_employees
from employees sub
join employees sup
on sub.manager_id = sup.employee_id
having count(sub.employee_id) > 6
group by sup.employee_id
order by sup.employee_id desc;
```

Result:  
<img width="244" alt="Screen Shot 2022-08-04 at 23 13 59" src="https://user-images.githubusercontent.com/59098085/182987076-f7f52986-a57c-46e5-8a4d-8bbbbb486efa.png">


#### 📌 C65: Write a query to generate a list of the 5 employees who have more time working for the company, applying the following conditions:        

<strong>

- The results include only the employee_id, first_name, last_name, hire_date, and commission_pct.

- The query takes into account only employees who have a commission_pct  defined  which is smaller than 0.3. 
</strong>


```sql
with hire_order as (
                    select 
                        employee_id, 
                        first_name, 
                        last_name, 
                        hire_date,
                        commission_pct,
                        rank() over (order by hire_date) as rn
                    from employees
                    where commission_pct < 0.3
)
select *
from hire_order
where rn <= 5;
```

Result:  
<img width="481" alt="Screen Shot 2022-08-04 at 23 39 09" src="https://user-images.githubusercontent.com/59098085/182989903-62dc8b50-fc4e-41c4-ab10-f5ad815b5ded.png">



#### 📌 C66: The email address of employees is expected to be constructed by concatenating the first letter of the first_name with the last_name.  Write a query to generate a list of employees whose registered email is different from the expected email, applying the following conditions:        

<strong>

- The results include only employees of these departments: Marketing, Purchasing, Executive.

- Take into account the fact that the email is stored in uppercase, so make sure the expected email is constructed in uppercase too.
</strong>


```sql
select
        employee_id,
        first_name,
        last_name,
        department_id,
        email,
        substr(first_name, 1,1) || upper(last_name) as expected_email
from employees
where department_id in (20,30,90)
and email != (substr(first_name, 1,1) || upper(last_name));
```

Result:  
<img width="553" alt="Screen Shot 2022-08-05 at 15 47 41" src="https://user-images.githubusercontent.com/59098085/183142070-8bf31a6d-7540-446c-aa08-b5e9e84d77fd.png">


#### 📌 C67: Write a query to generate a report of employees that includes a column with the last digits of the phone number,  applying the following conditions:         

<strong>

- The “last digits” of the phone number are those that are after the last dot (.)

- The results must include employees from the Marketing department.  Employees from other departments can be included only if they have a salary that is greater than or equal to 6000 and smaller than or equal to 6500.

- The results must be ordered by department_id.
</strong>


```sql
select
        employee_id,
        first_name,
        last_name,
        phone_number,
        substr(phone_number, instr(phone_number,'.',-1)+1) as last_digits,
        salary,
        department_id
from employees
where department_id = 20
or (salary >= 6000 and salary <= 6500)
order by department_id;
```

Result:  
<img width="649" alt="Screen Shot 2022-08-05 at 16 05 39" src="https://user-images.githubusercontent.com/59098085/183144460-1353879b-f2d1-4d21-a6a5-185bfdf7b471.png">


#### 📌 C68:  Write a query to list the names of the departments for which there are more than 5 employees,  applying the following conditions:   

<strong>

- The results must be ordered by the number of employees, in descending order.
</strong>


```sql
select department_name, count(employee_id) as employees
from departments d
left outer join employees e on d.department_id = e.department_id
having count(employee_id)>5
group by department_name
order by count(employee_id) desc;
```

Result:  
<img width="206" alt="Screen Shot 2022-08-20 at 12 35 33" src="https://user-images.githubusercontent.com/59098085/185754856-36075e90-e1c2-4f23-aed0-ac062a3f0bca.png">


#### 📌 C69: Write a query to list the id and names of departments that don’t have any employee,  applying the following conditions:    

<strong>

- The departments must be ordered alphabetically.
- Write 2 versions of the query:  the first one using a subquery and the second one using an aggregate function and an outer join.

</strong>

**Version 1** - Using Subquery <br/>
Solution 1

```sql
select 
    department_name, 
    department_id
from departments d
where  (
            select count(employee_id)
            from employees e 
            where e.department_id = d.department_id
            having count(employee_id) = 0
        ) = 0
group by department_id, department_name
order by department_name;
```

Solution 2

```sql
select 
    department_name, 
    department_id
from departments d
where not exists (
            select employee_id
            from employees e 
            where e.department_id = d.department_id
        )
group by department_id, department_name
order by department_name;
```


**Version 2** - Using Join and Agragate Function

```sql
select d.department_id, d.department_name
from departments d
left outer join employees e on d.department_id = e.department_id
having count(employee_id)=0
group by d.department_id, d.department_name
order by department_name;
```

Result:  
<img width="269" alt="Screen Shot 2022-08-20 at 13 09 29" src="https://user-images.githubusercontent.com/59098085/185756180-c10f3ada-f92a-4bf5-bcba-f13631c96ae1.png">


#### 📌 C70: Write a query to list all locations for which there is at least one employee,  applying the following conditions:    

<strong>The results must include the location id, the city and the number of employees for the location.

The results must be ordered by the number of employees.

Hint:  See the relational diagram you generated at the beginning of this practice session to understand the relationships between employees, departments and locations.</strong>


```sql
select 
    l.location_id,
    l.city,
    count(*)
from locations l
join departments d 
on l.location_id = d.location_id
join employees e 
on d.department_id = e.department_id
group by l.location_id, l.city
order by count(*);
```

Result:  
<img width="315" alt="Screen Shot 2022-08-22 at 15 51 29" src="https://user-images.githubusercontent.com/59098085/185996803-d6fe7710-36c1-4175-9acb-e24d0e4e8e94.png">



#### 📌 C71: The SELECT statement in the image below generates a list of the locations in Canada along with the number of departments in each location.  The query was written using the old syntax for joins. Your task is to re-write it using the new ANSI syntax for the outer join.  Make sure that your query returns the exact same results than the original one. 

<p align=center><img width="490" alt="Screen Shot 2022-08-04 at 10 38 39" src="https://user-images.githubusercontent.com/59098085/182861097-0dc0a380-59c1-4240-961e-c1b24d9a0321.png"></p>

```sql
  select l.location_id, l.city, count (d.location_id) as departments
    from locations l left join departments d on d.location_id = l.location_id
   where l.country_id = 'CA'
group by l.location_id, l.city;
```

Result:  
<img width="194" alt="Captura de tela 2022-09-09 135057" src="https://user-images.githubusercontent.com/59098085/189401186-082a9a08-b90a-4c23-af87-b9c3d2e65cd1.png">


#### 📌 C72: Write a query to generate a list of regions that includes the minimum and maximum salary for each region, taking into account the following conditions:    

<strong>
The results must include only regions that have employees

The regions must be ordered alphabetically</strong>


```sql
select region_name, min(e.salary) as min_salary, max(e.salary) as max_salary
from regions r
join countries c
    on r.region_id = c.region_id
join locations l
    on c.country_id = l.country_id
join departments d
    on d.location_id = l.location_id
join employees e
    on d.department_id = e.department_id
group by r.region_name
order by region_name;
```

Result:  
<img width="184" alt="Captura de tela 2022-09-09 143745" src="https://user-images.githubusercontent.com/59098085/189411490-a6a7d01c-537e-4138-bb01-6e567af3f15a.png">


#### 📌 C73: Write a query to generate a list of regions that includes the count of employees for each region, taking into account the following conditions:   

<strong>The results must include all regions

The regions must be ordered alphabetically</strong>


```sql
select region_name, count(e.employee_id)
from regions r
right outer join countries c
    on r.region_id = c.region_id
left outer join locations l
    on c.country_id = l.country_id
left outer join departments d
    on d.location_id = l.location_id
left outer join employees e
    on d.department_id = e.department_id
group by r.region_name
order by region_name;
```

Result:  
<img width="221" alt="Captura de tela 2022-09-09 144547" src="https://user-images.githubusercontent.com/59098085/189412669-2ea660d2-54ae-45f2-8945-b3aceae7dc37.png">



#### 📌 C74: Write a query to generate a list of employees along with the number of applications for which they have permissions, taking into account the following conditions:    

<strong>The results must include only employees with employee_id smaller than or equal to 105

Each application must be counted only once for each user.  Some users might have roles that end up giving them permissions for the same application more than once, so you need to do something to only count them once.

In addition to the column that counts the applications, there must be an additional column called “APPS_NOTE” that shows ‘5 OR LESS’ or ‘MORE THAN 5’ according to the number of apps counted.

The results must be ordered by employee_id

Hints: Some aggregate functions have a way to tell it to only take into account different or distinct values (aggregate functions lesson).   You need some kind of IF-THEN-ELSE logic to generate the apps_note column</strong>


```sql

```

Result:  



#### 📌 C75: Write a query to list all of the departments in the company along with 2 columns that show the number of active and inactive users in the company’s system, taking into account the following conditions:   

<strong>All departments must appear in the list even if they don’t have any user

The results must be ordered by department_id

Write 2 versions of the query, one using CASE expressions and one using the PIVOT clause

Hint: Sometimes you need to use subqueries to “prepare” your data to be pivoted.</strong>


```sql

```

Result:  



#### 📌 C76: The script you ran for this practice session created a view called "v_active_user_count" in your schema.  Views have not been covered yet, so by now just imagine that it is a table, and use it like that.  This view returns data about the number of active/inactive users per department, pivoted to display one column per department.  Your task is now using the Unpivot feature of Oracle SQL to produce the following output:   


```sql

```

Result:  



#### 📌 C77: Write a query to generate a list of the 2 more recently created users per department, taking into account the following conditions:     

<strong>If 2 or more users were created on the same date, they must be assigned the same ranking, which means that the results could actually include more than 2 users per department.

The final results must be ordered by department_id and by the rank assigned according to the user’s creation date.

Write one version of the query using an in-line view, and one using the WITH clause (also called, the subquery factoring clause).

Hint:  This could be called a “partitioned” top-n query.</strong>


```sql

```

Result:  



#### 📌 C78: The company is giving a raise on their salaries to employees who earn more than 10,000. Here is query that returns the list of employees that will get the raise, which includes a column for their new salary, which will be increased differently depending on the department where they work.  The query gives the correct results, but your task is to re-write using a CASE expression instead of the DECODE function.   

<p align=center><strong>Make sure that your query produces the exact same results as the original one.</strong></p>

<p align=center><img width="576" alt="Screen Shot 2022-08-04 at 10 47 19" src="https://user-images.githubusercontent.com/59098085/182863034-f650a55b-313c-4a88-9de9-25afdf394aff.png"></p>

```sql

```

Result:  



#### 📌 C79:  Write a query to list the employees of the “Executive” and “Finance” departments, with an additional column that tells us if the date on which the previous user that was created in the same department was created more than 1 year before.  Follow these requirements/guidelines:   

<strong>Consider a year as always being equal to 365 days.

If the previous user was created later than a year before, or there is no previous user in the department, return null for that column.

To understand the requirement, look at the row with employee_id=100 in the expected output below.  The user that was created before him was created on 23-JAN-2001, so since his user was created on 27-JUN-2003, the difference between the dates is more than one year.  If you see the row for employee_id=108, you can see that the previous user was created on 26-AUG-2002, so the difference is only one day, and thus, the column shows as null.

The SQL Developer instance used to generate the below output is configured to display nulls as "(null)", but you are not forced to do it the same way.  As long as the query returns null when it has to, how the null is displayed is not important.</strong>


```sql

```

Result:  



#### 📌 C80: Write a query to list the departments for which there are at least 2 employees who earn more than 10,000.     

<strong>The results must be ordered by department id.</strong>

```sql

```

Result:  



#### 📌 C81: The following statement produces correct results, but it doesn’t follow the practices recommended in this course to make code readable, and it uses the old syntax for joins.  Re-write it to use the new ANSI syntax and to adhere to the readability recommended practices.  Make sure that your version produces the exact same results as the original one.

<strong>Hint:  Besides the joins, there are 2 different areas of readability improvements that have been recommended in this course.</strong>

<p align=center><img width="524" alt="Screen Shot 2022-08-04 at 10 50 11" src="https://user-images.githubusercontent.com/59098085/182863674-d6609f28-d31d-4568-bd22-65d9cf667a1a.png"></p>

```sql

```

Result:  



#### 📌 C82: Write a query to get the number of employees and the sum of their salaries, who were hired per year in the Administration, Marketing and purchasing departments since year 2003.  

<strong>The number of employees hired must be displayed with 2 digits.

The sum of the salaries must be displayed with a comma as thousand separator and must include your local currency symbol.  The currency symbol must not be “fixed” or hardcoded in your query. It must use the local currency symbol as defined in your session settings.

The results must be ordered by department_id and year.</strong>


```sql

```

Result:  


#### 📌 C83: Write a query to generate a report of the number of employees per department at each level of the company’s hierarchy, but include only employees who are not managers.

<strong>Levels in which all employees are managers are not expected to be included in the result set.

Please order the results by level and department name. </strong>


```sql

```

Result:  




<br/>
