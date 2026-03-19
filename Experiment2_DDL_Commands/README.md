# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
---

Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

<img width="1187" height="394" alt="image" src="https://github.com/user-attachments/assets/7ffe7d1b-d0dd-4bf3-9a84-ccb0038a206b" />


**Question 2**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK(length(icom_id)=4),
FOREIGN KEY(icom_id) REFERENCES company(com_id) ON UPDATE CASCADE ON DELETE CASCADE);
```

**Output:**
<img width="1183" height="324" alt="image" src="https://github.com/user-attachments/assets/910c644c-31af-4165-baf1-ae7d6f16d0d7" />


**Question 3**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, Marks)
VALUES (205, 'Olivia Green', 'F', NULL, NULL);
INSERT INTO Student_details 
VALUES (207, 'Liam Smith', 'M', 'Mathematics', 85);
INSERT INTO Student_details 
VALUES (208, 'Sophia Johns', 'F', 'Science', NULL);
```

**Output:**

<img width="1179" height="208" alt="image" src="https://github.com/user-attachments/assets/b657847e-cc01-4109-b03d-58bd4c477818" />


**Question 4**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```sql
ALTER TABLE Employees
Add COLUMN salary INTEGER CHECK(salary > 0);
```

**Output:**
<img width="1192" height="256" alt="image" src="https://github.com/user-attachments/assets/fcd4cfec-fda9-438d-8e4a-a88bdabb9393" />


**Question 5**
---

Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.

```sql
CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
BonusAmount REAL CHECK(BonusAmount > 0),
BonusDate DATE,
Reason TEXT NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID));
```

**Output:**

<img width="1187" height="269" alt="image" src="https://github.com/user-attachments/assets/f19b883f-caf7-42b9-a1e2-ab118d23aec5" />


**Question 6**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID));
```

**Output:**

<img width="1028" height="190" alt="image" src="https://github.com/user-attachments/assets/645c2a92-ab27-427d-954b-c306b933433c" />


**Question 7**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
CREATE TABLE Attendance(
AttendanceID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
AttendanceDate DATE,
Status TEXT CHECK(Status IN('Present', 'Absent', 'Leave')),
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID));
```

**Output:**

<img width="1029" height="188" alt="image" src="https://github.com/user-attachments/assets/9b7d2e28-047f-469f-8f46-196c9450fc3e" />


**Question 8**
---
Write an SQL query to change the name of the column id to employee_id in the table employee.

```sql
ALTER TABLE employee
RENAME COLUMN id TO employee_id;
```

**Output:**

<img width="1187" height="222" alt="image" src="https://github.com/user-attachments/assets/6682a9f5-d21e-4747-8f29-447a68db958b" />


**Question 9**
---

Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
INSERT INTO BOOKS (ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished 
FROM Out_of_print_books;
```

**Output:**

<img width="1179" height="201" alt="image" src="https://github.com/user-attachments/assets/e5f3a9ad-04bb-4c73-84b4-89f53649071d" />


**Question 10**
---

Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.



```sql
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES(1, 'Sarah Parker', 'Manager', 'HR', 60000);
```

**Output:**

<img width="1184" height="163" alt="image" src="https://github.com/user-attachments/assets/6e22bcfa-d348-4e4e-be02-815a4c81d986" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
