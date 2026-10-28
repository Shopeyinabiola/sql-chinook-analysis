# Monthly Revenue with Running Total

**Business question:** How does revenue build up month by month?

**Skills used:** CTE, aggregation, window function (running total)

## Query
```sql
WITH monthly AS (
    SELECT YEAR(InvoiceDate) AS yr, MONTH(InvoiceDate) AS mth, SUM(Total) AS monthly_revenue
    FROM Invoice
    GROUP BY YEAR(InvoiceDate), MONTH(InvoiceDate)
)
SELECT yr, mth, monthly_revenue,
       SUM(monthly_revenue) OVER (ORDER BY yr, mth) AS running_total
FROM monthly;
```

## Result
![Monthly revenue with running total](../images/27-monthly-running-total.png.)

## Insight
The result covers 60 months, from 2021 to 2025. The final running total is 2,328.60, which equals the total of all invoices.
