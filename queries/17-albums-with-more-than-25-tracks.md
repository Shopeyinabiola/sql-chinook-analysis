# Albums with More Than 25 Tracks

**Business question:** Which albums are the largest by track count?

**Skills used:** CTE, joins, aggregation

## Query
```sql
WITH album_total AS (
    SELECT al.Title, ar.Name, COUNT(t.TrackId) AS track_count
    FROM Album al
    JOIN Artist ar ON ar.ArtistId = al.ArtistId
    JOIN Track t ON t.AlbumId = al.AlbumId
    GROUP BY al.Title, ar.Name
)
SELECT Title, Name, track_count
FROM album_total
WHERE track_count > 25
ORDER BY track_count ;
```

## Result
![Albums with more than 25 tracks](../images/17-albums-with-more-than-25-tracks.png.)

## Insight
Only 4 albums have more than 25 tracks. Lenny Kravitz's Greatest Hits is the largest with 57 tracks, followed by Chico Buarque's Minha Historia (34), Eric Clapton's Unplugged (30) and Lost, Season 3 (26).
