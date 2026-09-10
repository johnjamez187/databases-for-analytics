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

![Q1 Screenshot](screenshots/q1_document_count.png)

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

<img width="929" height="680" alt="Question 2" src="https://github.com/user-attachments/assets/521fdbac-8e81-4763-89fa-9952edd692c2" />


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

<img width="954" height="783" alt="Question 3" src="https://github.com/user-attachments/assets/4550460a-0839-420e-8415-e489733fce14" />


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

<img width="775" height="546" alt="Question 4" src="https://github.com/user-attachments/assets/17c3d4bb-f274-449d-9a99-affcde801195" />


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

<img width="765" height="578" alt="Question 5" src="https://github.com/user-attachments/assets/240bafd1-f6bb-45de-86cc-e757a7b2d154" />


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

<img width="710" height="481" alt="Question 6" src="https://github.com/user-attachments/assets/f00b5311-5b82-4c17-9bf8-9082155dc2e9" />


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

<img width="956" height="820" alt="Question 7" src="https://github.com/user-attachments/assets/b8e2e13c-b9c0-417f-a79c-cb23409c5ad5" />


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

<img width="876" height="841" alt="Question 8" src="https://github.com/user-attachments/assets/04ae2765-ed76-4430-9027-3761ce142673" />

