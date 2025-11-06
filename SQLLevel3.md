
# 📙 SQL – Level 3 (ADVANCED)

---

## 🧩 1️⃣ CTE (Common Table Expressions)

### 📖 Concept:
A **CTE** is a temporary result set that can be referred within a SELECT, INSERT, UPDATE, or DELETE statement.

### 💬 Example:
```sql
WITH AvgSalaryCTE AS (
  SELECT DeptID, AVG(Salary) AS AvgSalary
  FROM Employee
  GROUP BY DeptID
)
SELECT E.EmpName, E.Salary, A.AvgSalary
FROM Employee E
JOIN AvgSalaryCTE A ON E.DeptID = A.DeptID
WHERE E.Salary > A.AvgSalary;
```
→ Finds employees earning more than their department’s average.

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is CTE? | A temporary named result set used in query execution. |
| Difference between CTE and Subquery? | CTE improves readability and supports recursion. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can a CTE be recursive? | Yes, used for hierarchical data like org charts. |
| Does CTE improve performance? | Not always—mainly improves readability. |

---

## 🧩 2️⃣ Window Functions (OVER, PARTITION BY)

### 📖 Concept:
Window functions perform **calculations across a set of table rows** related to the current row.

### 💬 Example:
```sql
SELECT EmpName, DeptID, Salary,
  RANK() OVER (PARTITION BY DeptID ORDER BY Salary DESC) AS RankInDept
FROM Employee;
```
→ Ranks employees based on salary within each department.

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is PARTITION BY? | Divides result set into groups (like GROUP BY) for window functions. |
| What is ROW_NUMBER()? | Assigns sequential number to rows. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Difference between RANK() and DENSE_RANK()? | RANK skips numbers for ties; DENSE_RANK doesn’t. |
| Can we use window function in WHERE clause? | No, must use in SELECT or ORDER BY. |

---

## 🧩 3️⃣ Recursive Queries

### 📖 Concept:
Used to query **hierarchical or tree-like data** (like employees reporting to managers).

### 💬 Example:
```sql
WITH EmployeeHierarchy AS (
  SELECT EmpID, EmpName, ManagerID
  FROM Employee
  WHERE ManagerID IS NULL
  UNION ALL
  SELECT E.EmpID, E.EmpName, E.ManagerID
  FROM Employee E
  INNER JOIN EmployeeHierarchy EH ON E.ManagerID = EH.EmpID
)
SELECT * FROM EmployeeHierarchy;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is recursive query? | A query that calls itself using CTE. |
| Where it’s used? | To fetch parent-child relationships. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| How do you stop infinite recursion? | Use WHERE or MAXRECURSION limit. |

---

## 🧩 4️⃣ Pivot and Unpivot

### 📖 Concept:
Used to **rotate rows into columns (PIVOT)** and **columns into rows (UNPIVOT)**.

### 💬 Example (PIVOT):
```sql
SELECT * FROM
(SELECT DeptID, Salary FROM Employee) AS Source
PIVOT (
  AVG(Salary) FOR DeptID IN ([10], [20], [30])
) AS PivotTable;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is PIVOT used for? | To convert rows into columns. |
| What is UNPIVOT? | Converts columns into rows. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can we use aggregate in PIVOT? | Yes, mandatory (like AVG, SUM). |

---

## 🧩 5️⃣ Temporary Tables

### 📖 Concept:
Temporary tables store intermediate results for a session or transaction.

### 💬 Example:
```sql
CREATE TABLE #TempEmp (
  EmpID INT, EmpName VARCHAR(50), Salary DECIMAL(10,2)
);

INSERT INTO #TempEmp SELECT EmpID, EmpName, Salary FROM Employee WHERE Salary > 50000;
SELECT * FROM #TempEmp;
DROP TABLE #TempEmp;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is a temporary table? | A table that exists temporarily for a session. |
| Types? | Local (#Temp) and Global (##Temp). |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| When does local temp table get deleted? | When the session ends. |

---

## 🧩 6️⃣ Performance Tuning (Execution Plan & Indexing)

### 📖 Concept:
Optimization of SQL queries for faster performance using indexes, execution plans, and query refactoring.

### 💬 Example:
```sql
EXPLAIN SELECT * FROM Employee WHERE Salary > 60000;
```
→ Shows query plan to analyze bottlenecks.

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is an execution plan? | A roadmap of how SQL engine executes a query. |
| What slows down SQL queries? | Missing indexes, large joins, non-sargable queries. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| What is sargable query? | Query that can use index efficiently. |
| What is clustered index scan? | Reading entire table (less efficient). |

---

## 🧩 7️⃣ Normalization & Denormalization

### 📖 Concept:
- **Normalization** reduces data redundancy.
- **Denormalization** improves query performance by combining tables.

| Normal Form | Description |
|--------------|-------------|
| 1NF | Atomic values (no repeating groups) |
| 2NF | Every non-key depends on full primary key |
| 3NF | No transitive dependency |

### 💬 Example:
- 1NF: Each cell holds one value.  
- 2NF: Split Employee and Department tables.  
- 3NF: Remove derived fields (like total salary).

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is normalization? | Process to minimize redundancy and improve data integrity. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Does normalization improve performance? | Improves data consistency, not always performance. |

---

## 🧩 8️⃣ Advanced Joins (CROSS JOIN, SELF JOIN, APPLY)

### 📖 Concept:
- **CROSS JOIN**: Cartesian product of two tables.
- **SELF JOIN**: Join same table with itself.
- **APPLY (CROSS APPLY / OUTER APPLY)**: Used with table-valued functions.

### 💬 Example (CROSS APPLY):
```sql
SELECT D.DeptName, E.EmpName
FROM Department D
CROSS APPLY (
  SELECT TOP 1 EmpName FROM Employee WHERE DeptID = D.DeptID ORDER BY Salary DESC
) E;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| What is CROSS APPLY? | Applies table-valued function for each row of outer table. |
| Difference between CROSS JOIN and INNER JOIN? | CROSS JOIN gives all combinations, INNER JOIN filters on condition. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| Can CROSS JOIN cause performance issues? | Yes, large datasets multiply quickly. |

---

## 🧩 9️⃣ JSON & XML Handling

### 📖 Concept:
Modern SQL supports **storing and querying JSON or XML data**.

### 💬 Example (JSON):
```sql
SELECT JSON_VALUE(@json, '$.Employee.Name') AS EmpName;
```

### 💬 Example (XML):
```sql
SELECT EmpData.value('(/Employee/Name)[1]', 'VARCHAR(50)') AS EmpName
FROM EmployeeXML;
```

### 💬 Q&A:
| Question | Answer |
|-----------|---------|
| Can we store JSON in SQL? | Yes, using NVARCHAR and JSON functions. |

#### 🔁 Cross Question:
| Cross Question | Answer |
|----------------|---------|
| What’s the advantage of JSON column? | Flexibility for semi-structured data. |

---

## 🧩 🔟 Common Interview Scenarios

| Scenario | SQL Concept Used |
|-----------|------------------|
| Top N employees by salary per department | Window Functions |
| Hierarchical org chart | Recursive CTE |
| Compare sales across months | Self Join |
| Convert rows to columns | Pivot |
| Data audit on changes | Trigger |
| Performance tuning | Indexing + Execution Plan |

---

## 🧠 Practice Questions

1. Write a recursive query to display employee-manager hierarchy.  
2. Use window function to rank top 3 employees by salary in each department.  
3. Create a pivot table showing avg salary by department.  
4. Demonstrate normalization up to 3NF.  
5. Create function to return JSON output of employee details.  
6. Show execution plan for high-salary filter query.  
7. Use CROSS APPLY to fetch top 1 employee per department.  
8. Write trigger to store old salary when salary is updated.  
9. Write query to calculate cumulative salary using window function.  
10. Use CTE to find all subordinates of a manager.

---

## ✅ Summary

| Topic | Key Idea |
|--------|-----------|
| CTE | Temporary named query block |
| Window Functions | Perform row-level analytics |
| Recursive Query | Hierarchical data |
| Pivot | Rotate rows/columns |
| Temp Tables | Store session data |
| Performance | Optimize queries |
| Normalization | Reduce redundancy |
| Advanced Joins | Special join scenarios |
| JSON/XML | Handle semi-structured data |
| Scenarios | Real-world SQL problems |

