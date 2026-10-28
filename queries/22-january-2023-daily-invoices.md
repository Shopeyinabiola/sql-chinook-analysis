# January 2023 Daily Invoice Count

**Business question:** How many invoices were issued on each day of January 2023, including days with none?

**Skills used:** Recursive CTE (date generation), LEFT JOIN

## Query
```sql
WITH RECURSIVE date_series AS (
    SELECT DATE('2023-01-01') AS the_date
    UNION ALL
    SELECT DATE_ADD(the_date, INTERVAL 1 DAY)
    FROM date_series
    WHERE the_date < '2023-01-31'
)
SELECT ds.the_date, COUNT(i.InvoiceId) AS invoice_count
FROM date_series ds
LEFT JOIN Invoice i ON DATE(i.InvoiceDate) = ds.the_date
GROUP BY ds.the_date
ORDER BY ds.the_date;
```

## Result
![January 2023 daily invoice count](../images/22-january-2023-daily-invoice-count.png.)

## Insight
Only 6 of the 31 days had an invoice (7 invoices in total). The other 25 days show a count of 0, and a plain GROUP BY on the Invoice table would have hidden them.
