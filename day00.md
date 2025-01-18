## Day 00

#### Exercise 00 - First steps into SQL world
Let’s make our first task. Please make a select statement which returns all person's names and person's ages from the city ‘Kazan’.

```sql
SELECT * FROM person WHERE address = 'Kazan'
```
![alt text](image-2.png)


#### Exercise 01 - First steps into SQL world
Please make a select statement which returns names , ages for all women from the city ‘Kazan’. Yep, and please sort result by name.

```sql
SELECT * FROM person WHERE address='Kazan' AND gender='female'
ORDER BY name
```
![alt text](image-3.png)

#### Exercise 02 - First steps into SQL world
Please make 2 syntax different select statements which return a list of pizzerias (pizzeria name and rating) with rating between 3.5 and 5 points (including limit points) and ordered by pizzeria rating.

```sql
SELECT * FROM pizzeria WHERE rating>=3.5 AND rating<=5
ORDER BY rating
```
![alt text](image-2.png)


#### Exercise 03: First steps into SQL
Please make a select statement which returns the person's identifiers (without duplication) who visited pizzerias in a period from 6th of January 2022 to 9th of January 2022 (including all days) or visited pizzeria with identifier 2. Also include ordering clause by person identifier in descending mode.

```sql
SELECT * FROM person_visits WHERE visit_date BETWEEN '2022-01-06' AND '2022-01-09' AND pizzeria_id=2
ORDER BY person_id desc
```
![alt text](image-7.png)


#### Exercise 04 - First steps into SQL world
Please make a select statement which returns one calculated field with name ‘person_information’ in one string like described in the next sample:

`Anna (age:16,gender:'female',address:'Moscow')`

Finally, please add the ordering clause by calculated column in ascending mode.
Please pay attention to quote symbols in your formula!

```sql
SELECT concat('age:',age,',gender:',gender,',address:',address) AS person_information
FROM person 
```
![alt text](image-8.png)

#### Exercise 05 - First steps into SQL world
Please make a select statement which returns person's names (based on internal query in `SELECT` clause) who made orders for the menu with identifiers 13 , 14 and 18 and date of orders should be equal 7th of January 2022. Be aware with "Denied Section" before your work.

Please take a look at the pattern of internal query.

    SELECT 
	    (SELECT ... ) AS NAME  -- this is an internal query in a main SELECT clause
    FROM ...
    WHERE ...

```sql

```