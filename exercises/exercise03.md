# Exercise 03: MongoDB – Document Queries and Analysis

- Name:
- Course: Database for Analytics
- Module: 3
- Database Used: MongoDB
- Dataset: `restaurants-json.json`

---

## Instructions

- Import the provided `restaurants-json.json` file into MongoDB.
- All commands must be **executed by you** in the MongoDB shell or MongoDB Compass.
- For each query:
  - Include the MongoDB command in a fenced code block
  - Include a **screenshot** showing the command and its result
- Store screenshots in the `screenshots/` folder and embed them below each answer.

---

## Question 1

When importing the documents from `restaurants-json.json`,
**how many documents were imported into your collection**?

### Answer

25358

### Screenshot

<img width="991" height="830" alt="Question 1" src="https://github.com/user-attachments/assets/49cdc146-a84a-419b-9d16-6fa027b11eb7" />



_Show evidence of how you determined this (for example, a count query)._

```javascript
// Your MongoDB command here
```

![Exercise 3 Question 1](screenshots/Exercise%203%20Question%201.png)


---

## Question 2

Before writing queries on the data,
**what command** do you use to set the
**MongoDB shell to operate on the `44661` database**?

### MongoDB Command

```javascript
use("44661")
```

### Screenshot

![Exercise 3 Question 2](screenshots/Exercise%203%20Question%202.png)


---

## Question 3

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**locate all documents in the `"Queens"` borough**.

### MongoDB Query

```javascript
db.restaurants.find({ borough: "Queens" })
```

### Screenshot

![Exercise 3 Question 3](screenshots/Exercise%203%20Question%203.png)


---

## Question 4

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants in the `"Queens"` borough**.

### MongoDB Query

```javascript
db.restaurants.countDocuments({ borough: "Queens"})
```

### Screenshot

![Exercise 3 Question 4](screenshots/Exercise%203%20Question%204.png)


---

## Question 5

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants** in the `"Queens"` borough
**whose cuisine is `"Hamburgers"`**.

### MongoDB Query

```javascript
db.restaurants.countDocuments({
  borough: "Queens",
  cuisine: "Hamburgers"
})
```

### Screenshot

![Exercise 3 Question 5](screenshots/Exercise%203%20Question%205.png)


---

## Question 6

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants in Zipcode `10460`**.

_Hint: Look up how to query **embedded documents**._

### MongoDB Query

```javascript
db.restaurants.countDocuments({
  borough: "Queens",
  cuisine: "Hamburgers"
})
```

### Screenshot

![Exercise 3 Question 6](screenshots/Exercise%203%20Question%206.png)



---

## Question 7

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**display only the names of restaurants in Zipcode `10460`**.

_Hint: Look up how to **project fields** in MongoDB._

Your output should resemble:

```json
{ name: "Wild Asia" }
{ name: "Terrace Cafe" }
{ name: "African Terrace" }
{ name: "Cool Zone" }
{ name: "Beaver Pond" }
...
```

### MongoDB Query

```javascript
db.restaurants.find(
  { "address.zipcode": "10460" },
  { _id: 0, name: 1 }
)
```

### Screenshot

![Exercise 3 Question 7](screenshots/Exercise%203%20Question%207.png)

---

## Question 8

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**display only the names of restaurants whose name contains `"IHOP"`**,
ignoring case.

Your results should include:

- `"Ihop"`
- `"Ihop Restaurant"`

### MongoDB Query

```javascript
db.restaurants.find(
  { name: { $regex: "IHOP", $options: "i" } },
  { _id: 0, name: 1 }
)
```

### Screenshot

![Exercise 3 Question 8](screenshots/Exercise%203%20Question%208.png)
