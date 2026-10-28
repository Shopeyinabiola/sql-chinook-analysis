# Average Invoice per Year

**Business question:** How does the average invoice value change from year to year?

**Skills used:** Aggregation, GROUP BY, date functions

## Query
```sql
SELECT YEAR(InvoiceDate) AS invoice_year, ROUND(AVG(Total), 2) AS avg_invoice
FROM Invoice
GROUP BY YEAR(InvoiceDate)
ORDER BY invoice_year;
```

## Result
![Average invoice per year](../images/05-Average-Invoice-per-year.png.)

## Insight
The average invoice stays between 5.42 and 5.80 from 2021 to 2025, peaking in 2022. Customers spend a similar amount per order every year.
