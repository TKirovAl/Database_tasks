## Day 00

#### Exercise 00 - First steps into SQL world
Let’s make our first task. Please make a select statement which returns all person's names and person's ages from the city ‘Kazan’.

```sql
SELECT * FROM person WHERE city = 'Kazan'
```
Result:
![alt text](screen/image-1.png)
### Instead of "City" I put "Address"


## Exercise 01 - First steps into SQL world
Please make a select statement which returns names , ages for all women from the city ‘Kazan’. Yep, and please sort result by name.
```sql
SELECT name, age FROM person WHERE address = 'Kazan' and gender = 'female'
ORDER BY age DESC;
```
result:
![alt text](screen/image.png)

## Exercise 02 - First steps into SQL world
Please make 2 syntax different select statements which return a list of pizzerias (pizzeria name and rating) with rating between 3.5 and 5 points (including limit points) and ordered by pizzeria rating.
- the 1st select statement must contain comparison signs  (<=, >=)
- the 2nd select statement must contain `BETWEEN` keyword

```sql
SELECT * FROM pizzeria WHERE rating >= 3.5 and rating <= 5
ORDER BY rating DESC;
```
result with "<= and =>":
![alt text](screen/image-4.png)

```sql
SELECT * FROM pizzeria WHERE rating BETWEEN 3.5 and 5
ORDER BY name ASC;
```
result with BETWEEN:
![alt text](screen/image-5.png)

## Exercise 03 - First steps into SQL world
Please make a select statement which returns the person's identifiers (without duplication) who visited pizzerias in a period from 6th of January 2022 to 9th of January 2022 (including all days) or visited pizzeria with identifier 2. Also include ordering clause by person identifier in descending mode.

```sql
SELECT person_id
FROM person_visits WHERE visit_date = '2022-01-09'and pizzeria_id = 2
order by person_id DESC
```
result: 
![alt text](screen/image-6.png)

## Exercise 04 - First steps into SQL world
Please make a select statement which returns one calculated field with name ‘person_information’ in one string like described in the next sample:

`Anna (age:16,gender:'female',address:'Moscow')`

Finally, please add the ordering clause by calculated column in ascending mode.
Please pay attention to quote symbols in your formula!

```sql
SELECT concat('age: ', age, 'gender: ', gender, 'address: ', address) AS person_id
FROM person 
```
result:
![alt text](screen/image-10.png)

## Exercise 05 - First steps into SQL world
Please make a select statement which returns person's names (based on internal query in `SELECT` clause) who made orders for the menu with identifiers 13 , 14 and 18 and date of orders should be equal 7th of January 2022. Be aware with "Denied Section" before your work.

```sql
Select name
from person
where id IN
	(select person_id from person_order
	WHERE order_date = '2022-01-07'and menu_id IN(13, 14, 18)
)
```
result:
![alt text](screen/image.png)

## Exercise 06 - First steps into SQL world
Please use SQL construction from Exercise 05 and add a new calculated column (use column's name ‘check_name’) with a check statement (a pseudo code for this check is presented below) in the `SELECT` clause.

```sql
SELECT name, 
CASE	
	WHEN EXISTS (SELECT 1 FROM person_order WHERE person_order.person_id = person_id
	AND menu_id IN(13, 14, 18)
	AND order_date = '2022-01-07')
	THEN 'Has Order'
	ELSE 'No Order'
	END AS check_name 
	FROM person 
	WHERE
	id IN (SELECT person_id 
		  FROM person_order
		  WHERE menu_id IN(13, 14, 18)
		  AND order_date = '2022-01-07'
		  );
```
result:
![alt text](screen/image-1.png)

## Exercise 07 - First steps into SQL world
Let’s apply data intervals for the `person` table. 
Please make a SQL statement which returns a person's identifiers, person's names and interval of person’s ages (set a name of a new calculated column as ‘interval_info’) based on pseudo code below. 

    if (age >= 10 and age <= 20) then return 'interval #1'
    else if (age > 20 and age < 24) then return 'interval #2'
    else return 'interval #3'

and yes...please sort a result by ‘interval_info’ column in ascending mode.

```sql
SELECT 
    id,
    name,
    CASE 
        WHEN age >= 10 AND age <= 20 THEN 'interval #1'
        WHEN age > 20 AND age < 24 THEN 'interval #2'
        ELSE 'interval #3'
    END AS interval_info
FROM person
ORDER BY interval_info ASC;
```
result:
![alt text](screen/image-2.png)

## Exercise 08 - First steps into SQL world
Please make a SQL statement which returns all columns from the `person_order` table with rows whose identifier is an even number. The result have to order by returned identifier.

```sql
SELECT *
FROM person_order
WHERE id % 2 = 0
ORDER BY id ASC;
```
result:
![alt text](screen/image-3.png)

## Exercise 09 - First steps into SQL world
Please make a select statement that returns person names and pizzeria names based on the `person_visits` table with date of visit in a period from 07th of January to 09th of January 2022 (including all days) (based on internal query in `FROM` clause) .

Please take a look at the pattern of the final query.

    SELECT (...) AS person_name ,  -- this is an internal query in a main SELECT clause
            (...) AS pizzeria_name  -- this is an internal query in a main SELECT clause
    FROM (SELECT … FROM person_visits WHERE …) AS pv -- this is an internal query in a main FROM clause
    ORDER BY ...

Please add a ordering clause by person name in ascending mode and by pizzeria name in descending mode

```sql
SELECT 
    person.name,
    pizzeria.name
FROM person_visits
JOIN person ON person.id = person_visits.person_id
JOIN pizzeria ON pizzeria.id = person_visits.id
WHERE person_visits.visit_date BETWEEN '2022-01-07' AND '2022-01-09'
ORDER BY person.name ASC, pizzeria.name DESC;
```
result:
![alt text](screen/image-4.png)
