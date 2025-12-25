**RECURSIVE + INTERVAL** create a dimdate table with specific date range

```
WITH RECURSIVE cte AS ( SELECT '2025-01-01' AS dt
                        UNION ALL
                        SELECT dt + INTERVAL 1 DAY
                        FROM cte
                        WHERE dt < '2025-01-07'
                      )
```
