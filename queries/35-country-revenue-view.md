# Country Revenue (Views)

**Business question:** Which country generates the most revenue, using reusable views?

**Skills used:** Views, a view built on another view

## Query
```sql
CREATE VIEW customer_revenue AS
SELECT c.CustomerId, CONCAT(c.CustomerId, c.FirstName, c.Country) AS full_name, c.Country,
       SUM(il.UnitPrice * il.Quantity) AS total_spent
FROM Customer c
JOIN Invoice i ON i.CustomerId = c.CustomerId
JOIN InvoiceLine il ON il.InvoiceId = i.InvoiceId
GROUP BY c.CustomerId, c.FirstName, c.LastName, c.Country;

CREATE VIEW country_revenue AS
SELECT Country, COUNT(*) AS customer_count, SUM(total_spent) AS total_revenue
FROM customer_revenue
GROUP BY Country;

WITH ranked AS (
SELECT Country, customer_count, total_revenue,
RANK() OVER (ORDER BY total_revenue DESC) AS revenue_rank 
FROM country_revenue
)
SELECT * FROM ranked 
WHERE revenue_rank=1;
```

## Result
![Country revenue view](../images/35-country-revenue_view.png.)

## Insight
country_revenue is built on top of customer_revenue, a view on a view. The USA comes out on top with 13 customers and 523.06 in revenue.
