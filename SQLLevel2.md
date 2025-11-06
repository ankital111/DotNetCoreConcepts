# 📗 SQL – Level 2 (INTERMEDIATE)

---

## 🧩 1️⃣ JOINS (INNER, LEFT, RIGHT, FULL, SELF)

### 📖 Concept:
Joins combine data from **multiple tables** based on related columns.

| Type | Description | Example |
|------|--------------|----------|
| INNER JOIN | Returns matching records from both tables | Employees with a valid Dept |
| LEFT JOIN | Returns all records from left table + matches from right | All employees, even without dept |
| RIGHT JOIN | All records from right table + matches from left | All departments, even empty ones |
| FULL JOIN | All records from both sides (NULLs where no match) | All employees and departments |
| SELF JOIN | Table joined with itself | Find employees under same manager |

### 💬 Example:
```sql
SELECT E.EmpName, D.DeptName
FROM Employee E
INNER JOIN Department D
ON E.DeptID = D.DeptID;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a JOIN? | Combines rows from two or more tables based on a related column. |
| Difference between INNER and LEFT JOIN? | INNER shows only matched, LEFT shows all from left + matches. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we join more than 2 tables? | Yes, by chaining JOINs. |
| Can we use WHERE instead of JOIN? | For simple joins yes, but JOIN is more readable and flexible. |

---

## 🧩 2️⃣ Subqueries

### 📖 Concept:
A **subquery** is a query inside another query.

### 💬 Example:
```sql
SELECT EmpName, Salary
FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```
→ Finds employees earning more than average.

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a subquery? | A query nested within another query. |
| Types of subqueries? | Single-row, multi-row, correlated. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| What is a correlated subquery? | A subquery that depends on outer query for each row. |

---

## 🧩 3️⃣ Views

### 📖 Concept:
A **view** is a virtual table based on the result of a query.

### 💬 Example:
```sql
CREATE VIEW HighSalaryEmp AS
SELECT EmpName, Salary
FROM Employee
WHERE Salary > 50000;
```
Now you can use:
```sql
SELECT * FROM HighSalaryEmp;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a view? | A saved query that acts like a virtual table. |
| Can we update a view? | Yes, if it’s based on one table and no aggregates. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Difference between view and table? | Table stores data, view stores query definition. |
| Can we use indexes on views? | Not directly, but indexed views can be created in some DBs. |

---

## 🧩 4️⃣ Stored Procedures

### 📖 Concept:
Stored Procedures are **precompiled SQL statements** saved in database.

### 💬 Example:
```sql
CREATE PROCEDURE GetHighSalaryEmp
AS
BEGIN
  SELECT * FROM Employee WHERE Salary > 50000;
END;

EXEC GetHighSalaryEmp;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a stored procedure? | A reusable block of SQL logic stored in database. |
| Benefits? | Faster performance, reusability, security. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Difference between stored procedure and function? | Procedure can return multiple values, function returns one. |

---

## 🧩 5️⃣ Functions

### 📖 Concept:
Functions perform a task and return a value.

| Type | Description |
|------|--------------|
| Scalar | Returns single value |
| Table-Valued | Returns table |

### 💬 Example:
```sql
CREATE FUNCTION GetAnnualSalary(@MonthlySalary DECIMAL)
RETURNS DECIMAL
AS
BEGIN
  RETURN @MonthlySalary * 12;
END;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is user-defined function (UDF)? | A custom function created by user. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Difference between function and procedure? | Function returns value, procedure may or may not. |

---

## 🧩 6️⃣ Indexes

### 📖 Concept:
Indexes improve **query performance** by allowing fast data retrieval.

| Type | Description |
|------|--------------|
| Clustered | Sorts & stores data physically |
| Non-Clustered | Separate structure that points to data |

### 💬 Example:
```sql
CREATE INDEX idx_EmpName ON Employee(EmpName);
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is index? | Database structure to speed up queries. |
| Clustered vs Non-clustered? | Clustered sorts actual data, Non-clustered uses pointer. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| How many clustered indexes per table? | One (because data can be stored one way). |
| Can we create index on multiple columns? | Yes, composite index. |

---

## 🧩 7️⃣ Transactions & ACID Properties

### 📖 Concept:
A **transaction** is a sequence of operations performed as a single unit.

**ACID = Atomicity, Consistency, Isolation, Durability**

### 💬 Example:
```sql
BEGIN TRANSACTION;
UPDATE Account SET Balance = Balance - 1000 WHERE AccID = 1;
UPDATE Account SET Balance = Balance + 1000 WHERE AccID = 2;
COMMIT;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a transaction? | Group of SQL statements that execute as a unit. |
| What is COMMIT and ROLLBACK? | COMMIT saves, ROLLBACK cancels changes. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| What happens if power fails during transaction? | If COMMIT not done, transaction rolls back automatically. |

---

## 🧩 8️⃣ Triggers

### 📖 Concept:
Triggers are **automatic actions** executed when events occur (INSERT, UPDATE, DELETE).

### 💬 Example:
```sql
CREATE TRIGGER trg_Audit
ON Employee
AFTER INSERT
AS
INSERT INTO AuditLog VALUES ('New Employee Added', GETDATE());
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a trigger? | A database object that runs automatically on event. |
| Types? | AFTER, BEFORE, INSTEAD OF. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can trigger call another trigger? | Yes, but can cause nesting (avoid too deep). |

---

## 🧩 9️⃣ Set Operations

| Operation | Description |
|------------|--------------|
| UNION | Combines results (removes duplicates) |
| UNION ALL | Combines results (includes duplicates) |
| INTERSECT | Returns common rows |
| EXCEPT | Returns rows from first not in second |

### 💬 Example:
```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| Difference between UNION and UNION ALL? | UNION removes duplicates, UNION ALL keeps them. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use ORDER BY with UNION? | Yes, but only at the end of full query. |

---

## 🧩 🔟 CASE Expression

### 📖 Concept:
Acts like IF-THEN logic inside SQL.

### 💬 Example:
```sql
SELECT EmpName,
  CASE 
    WHEN Salary > 70000 THEN 'High'
    WHEN Salary BETWEEN 40000 AND 70000 THEN 'Medium'
    ELSE 'Low'
  END AS SalaryLevel
FROM Employee;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is CASE used for? | Conditional logic in SQL. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use CASE in WHERE clause? | Yes. |

---

## 🧠 Practice Questions

1. Write query to list employees even if they have no department.  
2. Find employees whose salary > average salary of their department.  
3. Create a view of top 5 highest-paid employees.  
4. Create a procedure to update employee salary by 10%.  
5. Create function to calculate yearly bonus (10% of salary).  
6. Create index on Employee(Salary).  
7. Demonstrate ACID using transactions.  
8. Write trigger to log deleted employees.  
9. Use UNION to merge customer and supplier names.  
10. Add CASE to classify employees by salary range.

---

## ✅ Summary

| Topic | Key Idea |
|--------|-----------|
| Joins | Combine data across tables |
| Subqueries | Nested queries for dynamic results |
| Views | Virtual tables from queries |
| Procedures | Reusable SQL logic |
| Functions | Return computed value |
| Indexes | Speed up data access |
| Transactions | Ensure data integrity |
| Triggers | Automate actions |
| Set Operations | Combine results |
| CASE | Conditional logic |

