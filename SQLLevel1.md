# 📘 SQL – Level 1 (BASICS)

## 🧩 1️⃣ What is SQL?

### 📖 Concept:
SQL stands for **Structured Query Language** — it is used to **store, retrieve, update, and manage** data in a **Relational Database**.

### 🧠 Example:
```sql
SELECT * FROM Employees;
```
→ This shows all data from the Employees table.

### 💬 Interview Q&A:
| Question | Answer |
|-----------|---------|
| What is SQL? | A standard language for managing relational databases. |
| What are types of SQL commands? | DDL, DML, DCL, TCL, DQL. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| What is DDL? | Data Definition Language – defines structure (CREATE, ALTER, DROP). |
| What is DML? | Data Manipulation Language – modifies data (INSERT, UPDATE, DELETE). |

---

## 🧩 2️⃣ Table, Rows, and Columns

### 📖 Concept:
A **table** is a collection of **rows (records)** and **columns (fields)**.

Example table:

| EmpID | EmpName | Salary | DeptID |
|-------|----------|--------|--------|
| 1 | Ankita | 60000 | 10 |
| 2 | Rohan | 70000 | 20 |

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a table? | Collection of data organized in rows and columns. |
| What is a row? | A single record. |
| What is a column? | A field representing attribute type (like name, salary). |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can a table have duplicate rows? | Yes, unless a constraint (like PRIMARY KEY) prevents it. |

---

## 🧩 3️⃣ Data Types

### 📖 Concept:
Data types define the **type of data** a column can store.

| Category | Example Data Types |
|-----------|--------------------|
| Numeric | INT, DECIMAL, FLOAT |
| String | CHAR, VARCHAR, TEXT |
| Date/Time | DATE, DATETIME, TIME |
| Binary | BLOB, VARBINARY |

### 💬 Example:
```sql
CREATE TABLE Employee (
  EmpID INT,
  EmpName VARCHAR(50),
  Salary DECIMAL(10,2),
  JoinDate DATE
);
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| Why use data types? | To store correct kind of data efficiently. |
| Difference between CHAR and VARCHAR? | CHAR = fixed length, VARCHAR = variable length. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Which is faster — CHAR or VARCHAR? | CHAR (but wastes space if values vary in length). |

---

## 🧩 4️⃣ Keys (Primary, Foreign, Composite)

### 📖 Concept:
Keys uniquely identify records and create relationships between tables.

| Key | Description |
|-----|--------------|
| Primary Key | Unique + Not Null |
| Foreign Key | Refers to Primary Key of another table |
| Composite Key | Combination of multiple columns as Primary Key |

### 💬 Example:
```sql
CREATE TABLE Department (
  DeptID INT PRIMARY KEY,
  DeptName VARCHAR(50)
);

CREATE TABLE Employee (
  EmpID INT PRIMARY KEY,
  EmpName VARCHAR(50),
  DeptID INT,
  FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a Primary Key? | A unique identifier for each record. |
| What is a Foreign Key? | A column that references another table’s Primary Key. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can a table have multiple Primary Keys? | No, but can have multiple columns in one Primary Key. |
| Can a table have multiple Foreign Keys? | Yes. |

---

## 🧩 5️⃣ Constraints

### 📖 Concept:
Rules that maintain **data integrity** in tables.

| Constraint | Purpose |
|-------------|----------|
| NOT NULL | Prevents null values |
| UNIQUE | No duplicate values |
| PRIMARY KEY | Unique + Not Null |
| FOREIGN KEY | Maintains referential integrity |
| CHECK | Validates values |
| DEFAULT | Provides default value |

### 💬 Example:
```sql
CREATE TABLE Employee (
  EmpID INT PRIMARY KEY,
  EmpName VARCHAR(50) NOT NULL,
  Salary DECIMAL(10,2) CHECK (Salary > 0),
  City VARCHAR(30) DEFAULT 'Mumbai'
);
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a constraint? | Rule that ensures data correctness. |
| Can we apply multiple constraints on same column? | Yes. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Difference between UNIQUE and PRIMARY KEY? | PRIMARY KEY = UNIQUE + NOT NULL; UNIQUE alone allows NULL. |

---

## 🧩 6️⃣ CRUD Operations

| Operation | SQL Command | Meaning |
|------------|--------------|----------|
| Create | INSERT | Add new data |
| Read | SELECT | Retrieve data |
| Update | UPDATE | Modify data |
| Delete | DELETE | Remove data |

### 💬 Example:
```sql
INSERT INTO Employee VALUES (1, 'Ankita', 50000, 10);
SELECT * FROM Employee;
UPDATE Employee SET Salary = 60000 WHERE EmpID = 1;
DELETE FROM Employee WHERE EmpID = 1;
```

---

## 🧩 7️⃣ SELECT with WHERE, ORDER BY, DISTINCT, LIKE

### 📖 Concept & Examples:
```sql
-- WHERE filters rows
SELECT * FROM Employee WHERE Salary > 40000;

-- ORDER BY sorts results
SELECT * FROM Employee ORDER BY Salary DESC;

-- DISTINCT removes duplicates
SELECT DISTINCT DeptID FROM Employee;

-- LIKE for pattern match
SELECT * FROM Employee WHERE EmpName LIKE 'A%';
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What does LIKE do? | Matches patterns using `%` and `_`. |
| What does DISTINCT do? | Removes duplicates from result. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use WHERE and ORDER BY together? | Yes. WHERE filters, ORDER BY sorts. |

---

## 🧩 8️⃣ Aggregate Functions (COUNT, SUM, AVG, MAX, MIN)

### 📖 Concept:
Used to perform calculations on data.

### 💬 Example:
```sql
SELECT COUNT(*) AS TotalEmp FROM Employee;
SELECT AVG(Salary) AS AvgSalary FROM Employee;
SELECT MAX(Salary) FROM Employee;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What are aggregate functions? | Functions that return a single value from multiple rows. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use WHERE with aggregate? | No, use HAVING for aggregate filters. |

---

## 🧩 9️⃣ GROUP BY and HAVING

### 📖 Concept:
`GROUP BY` groups rows, `HAVING` filters grouped results.

### 💬 Example:
```sql
SELECT DeptID, AVG(Salary)
FROM Employee
GROUP BY DeptID
HAVING AVG(Salary) > 50000;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| Difference between WHERE and HAVING? | WHERE filters rows, HAVING filters groups. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use HAVING without GROUP BY? | Yes, but not common. |

---

## 🧩 🔟 Aliases

### 📖 Concept:
Aliases give **temporary names** to columns or tables.

### 💬 Example:
```sql
SELECT EmpName AS Employee, Salary AS MonthlySalary
FROM Employee AS E;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is an alias? | A temporary name for readability. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can alias be used in WHERE clause? | No, it’s used only in SELECT or ORDER BY. |

---

## 🧠 Practice Questions

1. Create a table `Students` with columns: ID, Name, Marks, City.  
2. Insert 3 students into it.  
3. Write a query to display students with Marks > 80.  
4. Find total students per City.  
5. Get students whose name starts with 'A'.  
6. Find average marks of all students.  
7. Add a constraint to ensure Marks > 0.  
8. Retrieve distinct cities of students.  
9. Rename column Name as StudentName in query output.  
10. Delete all students from 'Delhi'.  

---

## ✅ Summary

| Topic | Key Point |
|--------|------------|
| SQL | Used to manage relational data |
| Table | Collection of rows and columns |
| Keys | Identify and relate data |
| Constraints | Ensure valid data |
| CRUD | Basic operations |
| WHERE | Filter rows |
| HAVING | Filter groups |
| ORDER BY | Sort results |
| GROUP BY | Aggregate by category |
| Alias | Rename columns/tables temporarily |
