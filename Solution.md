```sql

WITH ranked AS (
    SELECT
        country,
        age,
        RANK() OVER (PARTITION BY country ORDER BY age) AS rank_age,
        COUNT(*) OVER (PARTITION BY country) AS count_age
    FROM people
)

SELECT country, age
FROM ranked
WHERE rank_age = (count_age + 1) / 2           
   OR rank_age = count_age / 2                   
   OR rank_age = count_age / 2 + 1               
ORDER BY country, age;
```


| country | age |
|---------|-----|
| Germany |	6 |
| Germany | 54 |
| India |	33 | 
| India |	38 |
| Japan |	6 |
| Japan | 58 | 
| Malaysia |	44 |
| Poland | 34 |
| Poland |	45 |
| USA |	23 |
| USA | 32 |
