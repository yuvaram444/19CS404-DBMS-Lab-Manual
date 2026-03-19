# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table


<img width="467" height="211" alt="image" src="https://github.com/user-attachments/assets/f3a288bc-63d6-49b8-927d-7d0d6f890383" />


```sql
select STRFTIME('%Y' ,ValidityPeriod) as ValidityYear,count(PatientID) as TotalPatients
from Insurance 
Group by STRFTIME('%Y' ,ValidityPeriod)
order by ValidityYear;
```

## Output:

<img width="614" height="294" alt="image" src="https://github.com/user-attachments/assets/b654eb19-9f6d-4fd5-8aa4-65c9e441d23e" />


**Question 2**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table

<img width="985" height="159" alt="image" src="https://github.com/user-attachments/assets/2f11e7e8-1296-4803-85f3-ef6082066391" />

```sql
select Diagnosis,Count(*) as DiagnosisCount
from MedicalRecords
group by Diagnosis
order by DiagnosisCount DESC limit 1;
```

## Output:
<img width="793" height="227" alt="image" src="https://github.com/user-attachments/assets/12437fe0-e4f7-4f82-a9e7-ba92ae3fa0a2" />


**Question 3**
---
How many patients are covered by each insurance company?

Sample table:Insurance Table

<img width="310" height="203" alt="image" src="https://github.com/user-attachments/assets/ef11cc62-1329-4498-88c8-0fac80fca559" />

```sql
select InsuranceCompany,count(PatientID) as TotalPatients
from Insurance
group by InsuranceCompany;
```

## Output:

<img width="710" height="288" alt="image" src="https://github.com/user-attachments/assets/09172ed2-7225-4446-97c3-a0d9aa42f244" />


**Question 4**
---
Write a SQL query to find the shortest email address in the customer table?

Table: customer

<img width="275" height="179" alt="image" src="https://github.com/user-attachments/assets/4b22a0b1-8c26-476e-93a0-d539ad66b691" />


```sql
select name,email,min(LENGTH(email)) as min_email_length
from customer;
```

## Output:

<img width="976" height="231" alt="image" src="https://github.com/user-attachments/assets/81560a51-4fa8-4323-8bd4-5db237fa25b0" />


**Question 5**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

<img width="534" height="201" alt="image" src="https://github.com/user-attachments/assets/f2e13ea1-167c-43b7-9f06-5a2f1470f97c" />


```sql
SELECT avg(purch_amt) as AVERAGE
FROM orders;
```

## Output:

<img width="307" height="230" alt="image" src="https://github.com/user-attachments/assets/77d53974-38d4-4691-8ef3-39ae747db99e" />


**Question 6**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

<img width="327" height="174" alt="image" src="https://github.com/user-attachments/assets/cb8db054-bdac-46bd-b9d9-61a579351671" />


```sql
select count(age) as COUNT
from employee
where age>32;
```

## Output:

<img width="308" height="226" alt="image" src="https://github.com/user-attachments/assets/5c6c1216-6b47-49e4-b0a1-dadf4da2d395" />


**Question 7**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer

<img width="850" height="184" alt="image" src="https://github.com/user-attachments/assets/ee6bcdfd-b1cd-4ee7-8881-5d9fe7c53227" />

```sql

select count(*) as COUNT 
from customer
where city='Noida';
```

## Output:


<img width="308" height="229" alt="image" src="https://github.com/user-attachments/assets/e88e8744-0051-4458-862a-cf58c5f67541" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.

Sample table: employee

<img width="787" height="169" alt="image" src="https://github.com/user-attachments/assets/1925874d-10ea-4a0f-82ce-241faa0d1a2b" />


```sql
select age,MIN(income)
from employee
group by age
having min(income)< 400000;
```

## Output:


<img width="547" height="304" alt="image" src="https://github.com/user-attachments/assets/a8aae472-2148-435d-9d31-52c7a0516f04" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

Sample table: employee

<img width="787" height="174" alt="image" src="https://github.com/user-attachments/assets/e89ace46-921e-4752-b0d3-2657b95c9a0e" />

```sql
select age,MAX(income)
from employee
group by age
having MAX(income)>2000000;
```

## Output:


<img width="544" height="281" alt="image" src="https://github.com/user-attachments/assets/5be6dd98-98f5-43a4-99c6-015efc6d6cab" />


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1

<img width="787" height="159" alt="image" src="https://github.com/user-attachments/assets/1dcb0925-4b78-4356-b53e-7360a067dc58" />


```sql
select jdate,MIN(workhour)
from employee1
group by jdate
having min(workhour)<10;
```

## Output:


<img width="580" height="355" alt="image" src="https://github.com/user-attachments/assets/af46ca5a-da34-457e-b099-d429a26b29a3" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
