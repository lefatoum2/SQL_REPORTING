# SQL

### UNION ALL/JOIN

![imgt](./img_sql/table1.png)

```sql
-- Query season, country, and events for all summer events
SELECT 
	'summer' AS season, 
    country, 
    COUNT(DISTINCT event) AS events
FROM summer_games AS s
JOIN countries AS c
ON s.country_id = c.id
GROUP BY country
-- Combine the queries
UNION ALL
-- Query season, country, and events for all winter events
SELECT 
	'winter' AS season, 
    country, 
    COUNT(DISTINCT event) AS events
FROM winter_games AS w
JOIN countries AS c
ON w.country_id = c.id
GROUP BY country
-- Sort the results to show most events at the top
ORDER BY events DESC;
```
![img1](./img_sql/sql1.png)


## Sous-requêtes 

```sql
-- Add outer layer to pull season, country and unique events
SELECT 
	season, 
    country, 
    COUNT(DISTINCT event) AS events
FROM
    -- Pull season, country_id, and event for both seasons
    (SELECT 
     	'summer' AS season, 
     	country_id, 
     	event
    FROM summer_games
    UNION ALL
    SELECT 
     	'winter' AS season, 
     	country_id, 
     	event
    FROM winter_games) AS subquery
JOIN countries AS c
ON subquery.country_id = c.id
-- Group by any unaggregated fields
GROUP BY season, country
-- Order to show most events at the top
ORDER BY events DESC;
```

![img2](./img_sql/sql2.png)




## CASE 

![img3](./img_sql/Case140850.png)

```
SELECT 
	name,
    -- Output 'Tall Female', 'Tall Male', or 'Other'
	CASE when gender = 'F' and height < 175 then 'Tall Female'
    when gender = 'M' and height < 190 then 'Tall Male'
    else 'Other' END AS segment
FROM athletes;
```

![img3](./img_sql/Caseb141237.png)
