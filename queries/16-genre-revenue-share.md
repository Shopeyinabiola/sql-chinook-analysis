# Genre Revenue Share

**Business question:** Which genres contribute more than 5% of total revenue?

**Skills used:** CTE, aggregation, subqueries, percentages

## Query
```sql
WITH genre_revenue AS (
    SELECT g.Name, SUM(il.UnitPrice * il.Quantity) AS revenue
    FROM Genre g
    JOIN Track t ON t.GenreId = g.GenreId
    JOIN InvoiceLine il ON il.TrackId = t.TrackId
    GROUP BY g.GenreId, g.Name
)
SELECT Name, ROUND(revenue, 2) AS revenue,
       ROUND(revenue * 100 / (SELECT SUM(revenue) FROM genre_revenue), 1) AS pct
FROM genre_revenue
WHERE revenue > 0.05 * (SELECT SUM(revenue) FROM genre_revenue)
ORDER BY revenue DESC;
```

## Result
![Genre revenue share](../images/16-Genre-revenue-share.png.)

## Insight
Rock alone brings in 35.5% of revenue. Rock, Latin, Metal and Alternative & Punk together make up roughly 73% of the total, so revenue is concentrated in a few genres.
