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
**Exists**
```
select count(*) 
from payment p 
where  exists 
(select 1 from rental r where p.rental_id=r.rental_id);
```
**FETCH, Limit**


```
It sorts the rows by created_date, then skips the first 20 rows and returns the next 10 rows only.
In other words, it returns rows 21 to 30 from the ordered result set, which is commonly used for pagination (for example, showing one page of results at a time).

SELECT *
FROM table_name
ORDER BY created_date
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```
```
SELECT *
FROM table_name
ORDER BY created_date
LIMIT 10 OFFSET 20;
```
