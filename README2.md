```sql
select * from populations where life_expectancy > 1.15 * (select avg(life_expectancy) from populations
-- Select relevant fields from cities table
Select name, country_code, urbanarea_pop from cities
-- Filter using a subquery on the countries table
where name in (Select capital from countries where code is not null
ORDER BY urbanarea_pop DESC);


-- Find top nine countries with the most cities
SELECT countries.name AS country, COUNT(*) AS cities_num
FROM countries
LEFT JOIN cities
ON countries.code = cities.country_code
GROUP BY country
-- Order by count of cities as cities_num
ORDER BY cities_num DESC, country
LIMIT 9;

select countries.name as country, count(*) as cities_num
from countries
left join cities on  countries.code = cities.country_code
group by country 
Order by cities_num DESC, country LIMIT 9
```


```sql
-- Use coalesce
SELECT coalesce(industry, sector, 'Unknown') AS industry2,
       -- Don't forget to count!
       count(*) 
  FROM fortune500 
-- Group by what? (What are you counting by?)
 GROUP BY industry2
-- Order results to see most common first
 ORDER BY count DESC
-- Limit results to get just the one value you want
 LIMIT 1;
```
