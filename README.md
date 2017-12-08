# SQL AGGREGATE FUNCTIONS AND CASE WHEN
## SQL Queries with Aggregate functions such as SUM, AVG and COUNT. CASE WHEN and concatination of columns

```sql

SELECT
	INITCAP(first_name)||' '||COALESCE(INITCAP(middle_name), '')||' '||UPPER(last_name) AS full_name
FROM person
WHERE length(last_name)>= 7;

```
```sql

SELECT
  branch.id,
  country,
  city,
  COUNT(CASE WHEN iq = 156 THEN person.id END) AS num_of_highest
FROM branch LEFT JOIN person on branch.id = person.branch_id
GROUP BY
  branch.id,
  country,
  city;

```
```sql

SELECT
  branch.id,
  country,
  city,
  COUNT(CASE WHEN iq < 149 THEN person.id END) AS count_high,
  COUNT(CASE WHEN iq BETWEEN 149 AND 152 THEN person.id END) as count_very_high,
  COUNT(CASE WHEN iq > 152 THEN person.id END) as count_highest
FROM branch LEFT JOIN person ON branch.id = person.branch_id
GROUP BY
	branch.id,
  country,
  city;
  
```  
```sql

SELECT
	first_name,
  last_name,
  CASE
    	WHEN iq < 149 THEN 'high'
      WHEN iq BETWEEN 149 AND 152 THEN 'very high'
      WHEN iq > 152 THEN 'highest'
      ELSE 'missing'
  END as iq_rating
FROM person;

```
