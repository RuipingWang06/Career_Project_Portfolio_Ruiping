**RECURSIVE + INTERVAL** create a dimdate table with specific date range

```
WITH RECURSIVE cte AS ( SELECT CAST('2025-01-01' AS DATE) AS dt
                        UNION ALL
                        SELECT dt + INTERVAL 1 DAY
                        FROM cte
                        WHERE dt < CAST ('2025-01-07' AS DATE)
                      )
```
