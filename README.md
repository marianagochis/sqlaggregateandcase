# sqlaggregateandcase
--Exaple of SQL  queries with aggregate functions and case when
SELECT
	initcap(first_name)||' '||COALESCE(initcap(middle_name), '')||' '||UPPER(last_name) AS full_name
FROM person
WHERE length(last_name)>= 7;

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

SELECT
	branch.id,
    country,
    city,
    COUNT(CASE WHEN iq < 149 THEN person.id END) as count_high,
    COUNT(CASE WHEN iq BETWEEN 149 AND 152 THEN person.id END) as count_very_high,
    COUNT(CASE WHEN iq > 152 THEN person.id END) as count_highest
FROM branch LEFT JOIN person ON branch.id = person.branch_id
GROUP BY
	branch.id,
    country,
    city;
    
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
