# Employee Org Chart

**Business question:** What does the company's reporting structure look like, level by level?

**Skills used:** Recursive CTE (hierarchy)

## Query
```sql
WITH RECURSIVE Employee_Chart AS (
    SELECT EmployeeId, FirstName, LastName, ReportsTo, 1 AS level
    FROM Employee
    WHERE ReportsTo IS NULL
    UNION ALL
    SELECT e.EmployeeId, e.FirstName, e.LastName, e.ReportsTo, ec.level + 1
    FROM Employee e
    JOIN Employee_Chart ec ON e.ReportsTo = ec.EmployeeId
)
SELECT * FROM Employee_Chart
ORDER BY level;
```

## Result
![Employee org chart](../images/18.employee-org-chart.png.)

## Insight
The hierarchy has three levels: 1 person at the top, 2 managers (Sales and IT) at level 2, and 5 staff at level 3.
