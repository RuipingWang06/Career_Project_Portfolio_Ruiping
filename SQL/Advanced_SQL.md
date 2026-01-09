

**SQL Logic overview**

<img width="945" height="1031" alt="image" src="https://github.com/user-attachments/assets/ced0814b-d189-4305-bc26-49e8e8c64684" />

**Data Type**
Numerical : float,doubles,integer,boolean(0/1)
Non - Numberical : char,charater
timestamp : pay attention to the timezone 

**LEFT JOIN**

```
USE CASE

When a dimension table is used as the driving (top) table, it is usually to identify
whether dimension records exist in the fact table (e.g., coverage or usage analysis).
The join is typically:
Dimension.PK = Fact.FK

When a fact table is used as the driving (top) table, it is usually to enrich fact records
with descriptive attributes from dimension tables for reporting or analysis.

which film is out of inventory 

SELECT film.film_id,
       film.title,
       inventory_id
FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
WHERE inventory.film_id IS NULL;
```
**FULL JOIN** is used when you need to keep all records from both tables,including matched and unmatched rows.

**USE CASE**

Perform reconciliation or data quality checks (e.g., source vs target, old system vs new system).
<img width="621" height="414" alt="image" src="https://github.com/user-attachments/assets/378580b8-4c8e-4586-8652-7f9bd823353f" />


```
SELECT * 
FROM film_old O
FULL JOIN file_new N ON O.film_id = N.film_id
WHERE O.film_id IS NULL OR N.film_id IS NULL
```
**SELF JOIN**

**INNER JOIN**

**RECURSIVE + INTERVAL** 

```
---Create a dimdate table with specific date range,when there isn't a Date table in databases

WITH RECURSIVE cte AS ( SELECT CAST('2025-01-01' AS DATE) AS dt
                        UNION ALL
                        SELECT dt + INTERVAL 1 DAY
                        FROM cte
                        WHERE dt < CAST ('2025-01-07' AS DATE)
                      )
```
**COALESCE + ROUND + LAG()OVER(), LEAD()OVER(), ROW_NUMBER()OVER()**
```
SELECT cte.dt,
       COALESCE( sales.num_sales, ROUND((LAG(sales.num_sales) OVER() + LEAD( sales.num_sales)OVER())/2) AS sales_estimate
FROM cte LEFT JOIN sales ON cte.dt = sales.dt;
```
**EXISTS**
```
select count(*) 
from payment p 
where  exists 
(select 1 from rental r where p.rental_id=r.rental_id);
```
**FETCH, LIMIT**

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
**Sub query**

**USING**
```
SELECT c.name AS country, l.name AS language, official
FROM countries AS c
INNER JOIN languages AS l
USING (code)
```


**Function**

**extract** a spcific day/month from the payment_date

```
select extract (day from payment_date) from payment
select extract (Month from payment_date) from payment
select extract (dow from payment_date) from payment
```

**Mathmatical functions**
factorial/cube root/...

