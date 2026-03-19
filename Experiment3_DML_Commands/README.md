# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table

```sql
select Frequency,count(Frequency) as TotalPrescriptions
from Prescriptions
group by Frequency;
```

## Output:

<img width="741" height="514" alt="image" src="https://github.com/user-attachments/assets/98f2a758-b65a-43b1-847a-84ec15c863ed" />


**Question 2**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

```sql
select PatientID,count(AppointmentDateTime) as TotalAppointments
from Appointments
group by PatientID;
```

## Output:

<img width="679" height="242" alt="image" src="https://github.com/user-attachments/assets/3d78fc3f-d7e5-4ba1-b991-73db757483db" />


**Question 3**
---
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table

```sql
select PatientID,count(Medication) as TotalMedications
from Prescriptions
group by PatientID;
```

## Output:

<img width="654" height="360" alt="image" src="https://github.com/user-attachments/assets/ec05c33f-38ce-498e-8d99-ad12876040b9" />


**Question 4**
---
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer


```sql
select COUNT(grade) as COUNT
FROM customer;
```

## Output:

<img width="343" height="293" alt="image" src="https://github.com/user-attachments/assets/91f26cd9-3e72-45e7-be6c-434c43dfb4d1" />


**Question 5**
---
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

```sql
select avg(length(name)) as avg_name_length
from customer
where city='Chennai';
```

## Output:
<img width="416" height="281" alt="image" src="https://github.com/user-attachments/assets/540438dc-24fc-4103-8a2d-e4efcdaefd5f" />


**Question 6**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

```sql
select avg(length(email)) as avg_email_length 
from customer;
```

## Output:

<img width="430" height="274" alt="image" src="https://github.com/user-attachments/assets/2602ad5b-27d4-4a74-8e00-36cd9339f1b5" />


**Question 7**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

```sql
select min(purch_amt) as MINIMUM
from orders;
```

## Output:

<img width="337" height="287" alt="image" src="https://github.com/user-attachments/assets/1db28b7a-9b58-4533-8484-ced2de2076c3" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

Sample table: employee

```sql
select age,AVG(income)
from employee
group by age
having AVG(income) between 300000 and 500000;
```

## Output:

<img width="570" height="305" alt="image" src="https://github.com/user-attachments/assets/e5e67da3-03b0-446c-b715-984c88cfc72e" />


**Question 9**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```sql
select category_id,count(product_name)
from products
group by category_id
having category_id<3;
```

## Output:

<img width="727" height="328" alt="image" src="https://github.com/user-attachments/assets/6e0ce743-4f64-4cb8-ad3e-f4d4c9e1a915" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee



```sql
select city,SUM(income) as Income
from employee
group by city
having sum(income)>200000;
```

## Output:
<img width="535" height="502" alt="image" src="https://github.com/user-attachments/assets/c6d477d9-d255-4d15-bd52-d7616bd343a9" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
