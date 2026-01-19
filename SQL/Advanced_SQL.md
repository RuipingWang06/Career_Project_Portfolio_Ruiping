

**SQL Logic overview**

<img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/ced0814b-d189-4305-bc26-49e8e8c64684" />

**Data Type**
Numerical : float,doubles,integer,boolean(0/1)
Non - Numberical : char,charater
timestamp : pay attention to the timezone 


**GROUP BY**
```
SELECT 
    c.first_name, 
    c.last_name, 
    c.email, 
    SUM(p.amount) AS total_spent, 
    EXTRACT(year FROM MAX(p.payment_date)) AS last_payment_year 
FROM customer c 
JOIN payment p ON c.customer_id = p.customer_id -- Use JOIN to link the customer and payment tables
GROUP BY c.customer_id, c.first_name, c.last_name, c.email -- Group by customer to calculate total spending 
HAVING SUM(p.amount) > 200 -- Filter groups with total spending greater than 200 
ORDER BY total_spent DESC -- Sort by total spending from highest to lowest 
LIMIT 5; -- Return only the top 5 records
```


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

https://www.geeksforgeeks.org/postgresql/postgresql-self-join/

```
--Show the film Name which have the same runing time
SELECT
    f1.title AS Film_1,
    f2.title AS Film_2,
    f1.length AS Runtime
FROM
    film AS f1
INNER JOIN film AS f2 ON f1.film_id <> f2.film_id AND f1.length = f2.length;
```

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

It sorts the rows by created_date, then skips the first 20 rows and returns the next 10 rows only.
In other words, it returns rows 21 to 30 from the ordered result set, which is commonly used for pagination (for example, showing one page of results at a time).

```
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
**SUB QUERY**

**USING**
```
SELECT c.name AS country, l.name AS language, official
FROM countries AS c
INNER JOIN languages AS l
USING (code)
```
**FUNCTION**

**extract** a spcific day/month from the payment_date

```
select extract (day from payment_date) from payment
select extract (Month from payment_date) from payment
select extract (dow from payment_date) from payment
-- age calculation
EXTRACT(YEAR FROM AGE(CURRENT_DATE, p.birth_date))
```

**Mathmatical functions**

```
- Addition (+): Adds values together (e.g., 2 + 3 = 5).
- Subtraction (-): Subtracts one value from another (e.g., 2 - 3 = -1).
- Multiplication (*): Multiplies values (e.g., 2 * 3 = 6).
- Division (/): Performs division; note that integer division truncates the result (e.g., 4 / 2 = 2).
- Modulo (%): Returns the remainder of a division (e.g., 5 % 4 = 1).
- Exponentiation (^): Raises a number to a power (e.g., 2.0 ^ 3.0 = 8).
- Square Root (|/): Calculates the square root of a value.
- Cube Root (||/): Calculates the cube root of a value.
- Factorial (!): Calculates the factorial of a number (e.g., 5! = 120).
```

**Create Table**

Back up table (copy table structure and data)

```
CREATE TABLE table_a_copy AS
SELECT *
FROM table_a;

CREATE TABLE fact_reviews (
    review_key BIGINT GENERATED ALWAYS AS IDENTITY,
    author_id            TEXT,
    rating               NUMERIC,          
    is_recommended       BOOLEAN,          
    helpfulness          NUMERIC,          
    submission_time      DATE,             
    skin_type            TEXT
    skin_tone            TEXT
    sentiment_compound   NUMERIC,          
    sentiment_strength   NUMERIC,          
    sentiment_label      TEXT              
)
```
**DROP**

```
ALTER TABLE table_name
DROP COLUMN column_name;
```
**ALTER**

```
ALTER TABLE sephora_products
RENAME TO sephora_products_raw;
```
**INSERT**

When inserting data into a table with an auto-increment primary key, list all columns except the primary key. The primary key value will be generated automatically.

```
-- ~ : regex match, use to chlean data

INSERT INTO fact_reviews 
(author_id,
 rating,
 is_recommended,
 helpfulness,
 submission_time,
 skin_type,
 skin_tone,
 sentiment_compound,
 sentiment_strength,
 sentiment_label)
SELECT 
    author_id ,
    CAST(rating AS NUMERIC) AS rating,
    CASE 
        WHEN is_recommended NOT IN ('1','0') THEN NULL
        ELSE is_recommended = '1'
    END AS is_recommended,
    CASE 
        WHEN helpfulness ~ '^[0-9]+(\.[0-9]+)?$'
        THEN helpfulness::NUMERIC
        ELSE NULL
    END AS helpfulness, 
	CAST(submission_time AS DATE) AS submission_time,
    skin_type,
    CASE
        WHEN skin_tone IN (
            'dark','deep','ebony','fair','fairLight','light',
            'lightMedium','medium','mediumTan','olive',
            'porcelain','rich','tan'
        )
        THEN skin_tone
        ELSE ''
    END AS skin_tone,
    CAST(sentiment_compound AS NUMERIC)  AS sentiment_compound,
    CAST(sentiment_strength AS NUMERIC)  AS sentiment_strength,
    sentiment_label
FROM sephora_reviews_raw a
WHERE EXISTS (
    SELECT 1 
    FROM dim_sephora_products b 
    WHERE a.product_id = b.product_id
)
AND author_id ~ '^[0-9]+$'
AND rating ~ '^[0-9]+(\.[0-9]+)?$'
AND (submission_time IS NOT NULL
AND NOT (submission_time ~ '^\d{4}-\d{2}-\d{2}$'
    AND submission_time::date IS NOT NULL
  ));
```
