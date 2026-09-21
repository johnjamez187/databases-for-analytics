

- Name:
- Course: Database for Analytics
- Module:
- Database Used: `sqlda` (Sample Datasets)
- Tools Used: PostgreSQL (pgAdmin or psql)

---

## Instructions

- Use the **sqlda** database from the "Loading the Sample Datasets" instructions.
- For each SQL task:
  - Include your SQL in a fenced code block
  - Execute it and include a **screenshot** showing the query and results
- Store screenshots in the `screenshots/` folder and embed them below each answer.
- For explanation questions:
  - Write your answer in complete sentences
  - Include a screenshot if requested

---

## Question 1

Using the `sqlda` database, write the SQL needed
to show a **list of years** that emails were sent.

Your results should list years like this (order matters):

```text
year
2011
2013
2014
2015
2016
2017
2018
2019
```

### SQL

```sql
SELECT DISTINCT
    EXTRACT(YEAR FROM sent_date) AS year
FROM emails
ORDER BY year;
```



### Screenshot

![Question 1 Screenshot](<../screenshots/Exercise 5 Question 1.png>)



---

## Question 2

Using the `sqlda` database, write the SQL needed to
show the **number of messages sent by year**,
ordered by year (as shown in the prompt).

Output should resemble:

```text
count   year
...
```

### SQL

```sql
SELECT
    EXTRACT(YEAR FROM sent_date) AS year,
    COUNT(*) AS messages_sent
FROM emails
GROUP BY EXTRACT(YEAR FROM sent_date)
ORDER BY year;
```

### Screenshot

![Question 2 Screenshot](../screenshots/Exercise%205%20Question%202.png)

---

## Question 3

Using the `sqlda` database, write the SQL needed to show:

- the **sent date**
- the **opened date**
- the **interval** between the two

Only include emails that contain **both** a sent date and an opened date.

### SQL

```sql
SELECT
    sent_date,
    opened_date,
    opened_date - sent_date AS interval
FROM emails
WHERE sent_date IS NOT NULL
  AND opened_date IS NOT NULL;
```


### Screenshot

![Question 3 Screenshot](../screenshots/Exercise%205%20Question%203.png)

---

## Question 4

Using the `sqlda` database,
write the SQL needed to
show emails that contain an **opened date BEFORE the sent date**.

### SQL

```sql
SELECT
    sent_date,
    opened_date,
    opened_date - sent_date AS interval
FROM emails
WHERE opened_date IS NOT NULL
  AND sent_date IS NOT NULL
  AND opened_date < sent_date;
```

### Screenshot


![Question 4 Screenshot](../screenshots/Exercise%205%20Question%204.png)

---

## Question 5

Using the `sqlda` database:
there are **over 100 emails**
that contain an opened date **BEFORE** the sent date.

After looking at the data, **why is this the case?**

### Answer

There is probably a time zone difference between the two.





---

## Question 6

Using the `sqlda` database, explain in your own words what the following code does:

```sql
CREATE TEMP TABLE customer_points AS (
    SELECT
        customer_id,
        point(longitude, latitude) AS lng_lat_point
    FROM customers
    WHERE longitude IS NOT NULL
    AND latitude IS NOT NULL
);

CREATE TEMP TABLE dealership_points AS (
    SELECT
        dealership_id,
        point(longitude, latitude) AS lng_lat_point
    FROM dealerships
);

CREATE TEMP TABLE customer_dealership_distance AS (
    SELECT
       customer_id,
       dealership_id,
       c.lng_lat_point <@> d.lng_lat_point AS distance
    FROM customer_points c
    CROSS JOIN dealership_points d
);
```

### Answer

Created 3 separate, temporary, tables. This should be a distance relational data based on the point references, and it is separated by customer ids, dealership id, and distance from with the point from the dealership. 

---

## Question 7

Using the `sqlda` database,
write SQL to display an
**array of salespeople for each dealership**,
sorted by dealership.

For example - dealership 1 is below:

```text
"{""Fidell,Granville"",""Onele,Jereme"",""Sheriff,Lelia"",""McSpirron,Massimiliano"",""Rennick,Nadia"",""Mace,Eveleen"",""Oxteby,Dukie"",""Spong,Marcos"",""Wogden,Quent"",""Duny,Sandye"",""Loraine,Englebert"",""Meere,Ira"",""Gibbens,Cristine"",""Prine,Lyda"",""McCoughan,Sheff"",""Schule,Giselbert"",""McAndie,Eleen"",""Dosedale,Dorie"",""Nafziger,Shay""}"
```

### SQL

```sql
SELECT
    dealership_id,
    ARRAY_AGG(last_name || ' ' || first_name) AS salespeople
FROM salespeople
GROUP BY dealership_id
ORDER BY dealership_id;
```

### Screenshot

![Question 7 Screenshot](../screenshots/Exercise%205%20Question%207.png)

---

## Question 8

Using the `sqlda` database, write SQL to display:

- an **array of salespeople for each dealership**
- the **state** of the dealership
- the **number of salespeople** for the dealership

Sort by **state**.

Reference image:

![05-ExerciseArray](./instructions/05-ExerciseArray.jpg)

### SQL

```sql
SELECT
    d.dealership_id,
    d.state,
    ARRAY_AGG(s.first_name || ' ' || s.last_name) AS salespeople,
    COUNT(s.salesperson_id) AS number_of_salespeople
FROM dealerships AS d
JOIN salespeople AS s
    ON d.dealership_id = s.dealership_id
GROUP BY
    d.dealership_id,
    d.state
ORDER BY
    d.state;
```

### Screenshot

![Question 8 Screenshot](../screenshots/Exercise%205%20Question%208.png)

---

## Question 9

Using the `sqlda` database, write the SQL needed to convert
the **customers** table to **JSON**.

### SQL

```sql
SELECT row_to_json(customers)
FROM customers;
```

### Screenshot

![Question 9 Screenshot](../screenshots/Exercise%205%20Question%209.png)

---

## Question 10

Using the `sqlda` database, write SQL to display:

- an **array of salespeople for each dealership**
- the **state**
- the **number of salespeople**
- sorted by **state**

Then **convert this result to JSON**.

Reference image:

![05-ExerciseArray-1](./instructions/05-ExerciseArray-1.jpg)

### SQL

```sql
SELECT row_to_json(dealership_data)
FROM (
    SELECT
        d.dealership_id,
        d.state,
        ARRAY_AGG(s.first_name || ' ' || s.last_name) AS salespeople,
        COUNT(s.salesperson_id) AS number_of_salespeople
    FROM dealerships AS d
    JOIN salespeople AS s
        ON d.dealership_id = s.dealership_id
    GROUP BY
        d.dealership_id,
        d.state
    ORDER BY
        d.state
) AS dealership_data;
```

### Screenshot

![Question 10 Screenshot](../screenshots/Exercise%205%20Question%2010.png)
