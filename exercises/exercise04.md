# Exercise 04: Advanced SQL, Jupyter, and Visualization

- Name:
- Course: Database for Analytics
- Module:
- Database Used: World Database
- Tools Used: PostgreSQL, SQLAlchemy, Pandas, Jupyter Notebooks

---

## Instructions

- Complete each task using the **World database** installed earlier.
- For SQL questions:
  - Write the SQL command in a fenced code block
  - Execute the command and include a **screenshot of the results**
- For Jupyter Notebook questions:
  - Include the required Python statements
  - Include **screenshots of the notebook output**
- Store all screenshots in the `screenshots/` folder and embed them below each question.

---

## Question 1

Considering the World database, write a SQL statement that will
**display the names of countries**
that speak **more than two official languages**,
along with the **number of official languages spoken**.

- Sort the results by **number of languages**, from **most to least**.
- _Hint: There are fewer than 10 countries in the results._

### SQL

```sql
SELECT
    c.name AS country,
    COUNT(cl.language) AS official_languages
FROM country AS c
JOIN countrylanguage AS cl
    ON c.code = cl.countrycode
WHERE cl.isofficial = 'T'
GROUP BY c.name
HAVING COUNT(cl.language) > 2
ORDER BY official_languages DESC;
```

### Screenshot

<img width="940" height="911" alt="Question 1" src="https://github.com/user-attachments/assets/7c146dbf-2065-4bc1-bd85-6321daa15da9" />


---

## Question 2

Using **Jupyter Notebooks**, you must use the
`create_engine` command to connect to your database.

After the `create_engine` command is executed,
**what are the three statements** required to
execute the query from Question 1 and
**display the results in the notebook**?

### Python Code

```python

Define the SQL query

query = """
SELECT
    c.name AS country,
    COUNT(cl.language) AS official_languages
FROM country AS c
JOIN countrylanguage AS cl
    ON c.code = cl.countrycode
WHERE cl.isofficial = 'T'
GROUP BY c.name
HAVING COUNT(cl.language) > 2
ORDER BY official_languages DESC;
"""

Execute the query and store the results

df = pd.read_sql(query, engine)

Display the Results

display(df)

```

### Screenshot

<img width="566" height="393" alt="Question 2" src="https://github.com/user-attachments/assets/b7753b69-bc32-4fce-a959-2c065b7fd9bf" />


---

## Question 3

Using **Jupyter Notebooks**, write the Python code needed
to produce the following graph:

![countries.jpg](./instructions/04-countries.jpg)

(The graph shows country-level results derived from the World database.)

### Python Code

```python
df.plot(
    kind="bar",
    x="name",
    y="num_languages",
    rot=90
)
```

### Screenshot

<img width="734" height="843" alt="Question 3" src="https://github.com/user-attachments/assets/3ea3dc00-324a-478a-9760-77ab92fc8fb5" />

