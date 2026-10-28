# Customers Who Never Bought Jazz

**Business question:** Which customers have never purchased a Jazz track?

**Skills used:** Anti join (NOT EXISTS), multi-table joins

## Query
```sql
SELECT c.FirstName, c.LastName
FROM Customer c
WHERE NOT EXISTS (
    SELECT 1
    FROM Invoice i
    JOIN InvoiceLine il ON il.InvoiceId = i.InvoiceId
    JOIN Track t ON t.TrackId = il.TrackId
    JOIN Genre g ON g.GenreId = t.GenreId
    WHERE i.CustomerId = c.CustomerId AND g.Name = 'Jazz'
);
```

## Result
![Customers who never bought Jazz](../images/14-customers-who-never-bought-jazz.png.)

## Insight
27 of the 59 customers (about 46%) have never bought a Jazz track, which makes them a target group for Jazz promotions.
