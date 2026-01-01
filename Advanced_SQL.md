**RECURSIVE + INTERVAL** create a dimdate table with specific date range

```
WITH RECURSIVE cte AS ( SELECT CAST('2025-01-01' AS DATE) AS dt
                        UNION ALL
                        SELECT dt + INTERVAL 1 DAY
                        FROM cte
                        WHERE dt < CAST ('2025-01-07' AS DATE)
                      )
```
**COALESCE + ROUND + LAG()OVER(), ROW_NUMBER()OVER(),LEAD()OVER()**
```
SELECT cte.dt,
       COALESCE( sales.num_sales, ROUND((LAG(sales.num_sales) OVER() + LEAD( sales.num_sales)OVER())/2) AS sales_estimate
FROM cte LEFT JOIN sales ON cte.dt = sales.dt;
```
