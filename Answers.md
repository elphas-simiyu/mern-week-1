
 **1. Setup MongoDB**

#### Install MongoDB Locally or Use MongoDB Atlas

**Locally:**
- Install MongoDB Community Edition from [MongoDB's official site](https://www.mongodb.com/try/download/community).
- After installation, you can start the MongoDB server by running:
    ```
    mongod
    ```

**MongoDB Atlas:**
- Create a free MongoDB Atlas account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
- Create a cluster and connect to it using the provided connection string.
- Once connected, you can manage your database via MongoDB Atlas' web interface or through the MongoDB shell.

**Verify Installation:**
- After installation, run the following command to ensure MongoDB is correctly installed:
    ```
    mongo --version
    ```

---

### **2. Database and Collection Creation**

```javascript
// Connect to MongoDB (if using local MongoDB, just run `mongo` in the shell)
use library // Switch to the 'library' database (will create it if it doesn't exist)

// Create a collection 'books'
db.createCollection("books")
```

---

### **3. Insert Data**

I'm inserting 5 books with the following fields: `title`, `author`, `publishedYear`, `genre`, and `ISBN`.

```javascript
db.books.insertMany([
    { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Classic", ISBN: "9780743273565" },
    { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "9780451524935" },
    { title: "To Kill a Mockingbird", author: "Harper Lee", publishedYear: 1960, genre: "Classic", ISBN: "9780061120084" },
    { title: "The Catcher in the Rye", author: "J.D. Salinger", publishedYear: 1951, genre: "Classic", ISBN: "9780316769488" },
    { title: "The Hobbit", author: "J.R.R. Tolkien", publishedYear: 1937, genre: "Fantasy", ISBN: "9780547928227" }
]);
```

---

### **4. Retrieve Data**

**Retrieve all books:**
```javascript
db.books.find()
```

**Query books by a specific author (e.g., George Orwell):**
```javascript
db.books.find({ author: "George Orwell" })
```

**Find books published after the year 2000:**
```javascript
db.books.find({ publishedYear: { $gt: 2000 } })
```

---

### **5. Update Data**

**Update the `publishedYear` of a specific book (e.g., "The Hobbit"):**
```javascript
db.books.updateOne(
    { title: "The Hobbit" },
    { $set: { publishedYear: 1938 } }
)
```

**Add a `rating` field to all books with a default value:**
```javascript
db.books.updateMany(
    {},
    { $set: { rating: 5 } } // Default rating value of 5
)
```

---

### **6. Delete Data**

**Delete a book by its ISBN (e.g., ISBN "9780451524935"):**
```javascript
db.books.deleteOne({ ISBN: "9780451524935" })
```

**Remove all books of a particular genre (e.g., "Classic"):**
```javascript
db.books.deleteMany({ genre: "Classic" })
```

---

### **7. Data Modeling Exercise**

For the e-commerce platform, you should create collections for users, orders, and products.

**Example of a simple data model:**

- **Users Collection**: Contains information about customers.
  ```javascript
  db.users.insertOne({
      username: "john_doe",
      email: "john.doe@example.com",
      password: "hashed_password",
      createdAt: new Date()
  });
  ```

- **Orders Collection**: Contains orders made by users.
  ```javascript
  db.orders.insertOne({
      userId: ObjectId("user_object_id"),
      items: [
          { productId: ObjectId("product_object_id"), quantity: 2 },
          { productId: ObjectId("another_product_id"), quantity: 1 }
      ],
      orderDate: new Date(),
      status: "shipped"
  });
  ```

- **Products Collection**: Contains products that are available for purchase.
  ```javascript
  db.products.insertOne({
      name: "Laptop",
      price: 1200,
      stock: 50,
      description: "A high-performance laptop"
  });
  ```

---

### **8. Aggregation Pipeline**

- **Total number of books per genre:**
```javascript
db.books.aggregate([
    { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
])
```

- **Average published year of all books:**
```javascript
db.books.aggregate([
    { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
])
```

- **Top-rated book (assuming a `rating` field exists):**
```javascript
db.books.aggregate([
    { $sort: { rating: -1 } },
    { $limit: 1 }
])
```

---

### **9. Indexing**

Create an index on the `author` field:

```javascript
db.books.createIndex({ author: 1 })  // Ascending index
```

**Benefits of indexing in MongoDB:**
- **Improved Query Performance**: Indexes make queries faster by allowing MongoDB to quickly locate the data.
- **Efficiency**: Without indexes, MongoDB has to perform a collection scan, which is slower as the collection grows.
- **Optimized Reads**: Indexes are especially useful for queries that sort or filter by specific fields.

---

### **10. Testing**

- Use **MongoDB Shell** or **MongoDB Compass**  to test the data you've inserted, updated, or deleted.
- Verify that your queries return the expected results by running them and checking the output.

---


