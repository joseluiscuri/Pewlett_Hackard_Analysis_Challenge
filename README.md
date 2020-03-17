# Pewlett_Hackard_Analysis_Challenge

The following results were made using Pewlett Harckard's Employee Database.

The aim of this work is to get 3 objectives:
1. Number of individuals retiring
2. Number of individuals being hired
3. Number of individuals available for mentorship role

## 1- Individuals retiring: 108,958
Using 2 main rules to determine individual retiring:
1. Individuals being hired between 01/01/1985 and 12/31/1988
2. Individuals that are still working
This result was obtained using the following query:
 ```
SELECT 
emp.emp_no as EmployeeNumber,
emp.first_name ,
emp.last_name,
tt.title,
tt.from_date,
sl.salary
INTO ready_for_retirement
from employees as emp
INNER JOIN titles as tt ON tt.emp_no = emp.emp_no
INNER JOIN salaries as sl ON sl.emp_no = emp.emp_no
WHERE 1=1 
AND (hire_date BETWEEN '1985-01-01' AND '1988-12-31')
AND tt.to_date = '9999-01-01'
Order by tt.from_date DESC;
```
## 2- Number of titles retiring: 7
This result was obtained using the following query:
```
SELECT 
title, 
count(*) 
into titles_for_retirement
from ready_for_retirement
group by title;
```
## 3- Individuals available for mentorship role: 1,549
This result was obtained using the following query:
```    
SELECT 
emp.emp_no as EmployeeNumber,
emp.first_name ,
emp.last_name,
tt.title,
tt.from_date,
tt.to_date
INTO ready_for_mentor
from employees as emp
INNER JOIN titles as tt ON tt.emp_no = emp.emp_no
WHERE 1=1
AND (birth_date BETWEEN '1965-01-01' AND '1965-12-31')
AND to_date = '9999-01-01'
ORDER by from_date;
SELECT count(*) from ready_for_mentor;
```

Additionally, I would suggest to make an analysis of how people is getting promoted (by time, performance or any other metric) and identify which are the most critical elements. Also, I recommend to put in place an HR recruitment strategy alligned with the career path strategy to make it easier for recruiters to identify and assess the best timing for onboarding new employees.
