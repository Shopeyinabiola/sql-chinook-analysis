# Top Customer per Country

**Business question:** Who is the highest-spending customer in each country?

**Skills used:** CTE, window function (RANK with PARTITION BY)

## Query
```sql
WITH spend AS (
    SELECT c.CustomerId, c.Country, SUM(il.UnitPrice * il.Quantity) AS Spending
    FROM Customer c
    JOIN Invoice i ON i.CustomerId = c.CustomerId
    JOIN InvoiceLine il ON il.InvoiceId = i.InvoiceId
    GROUP BY c.CustomerId, c.Country
),
ranked AS (
    SELECT *, RANK() OVER (PARTITION BY Country ORDER BY Spending DESC) AS Spending_Rank
    FROM spend
)
SELECT * FROM ranked
WHERE Spending_Rank = 1;
```

## Result
![Top customer per country](../images/24-top-customer-per-country.png.)

## Insight
The result has 26 rows for 24 countries. RANK() keeps ties, so some countries show more than one customer at the top.
