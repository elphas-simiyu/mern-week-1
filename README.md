# mern-week-1
# MongoDB Setup and Run Instructions

This guide provides step-by-step instructions on how to set up and run MongoDB.

## Prerequisites

Before setting up MongoDB, ensure that you have the following installed:

- **MongoDB**:  
  Follow the installation guide for your operating system:
  - [MongoDB Installation Guide](https://www.mongodb.com/docs/manual/installation/)

- **MongoDB Compass (optional)**:  
  [MongoDB Compass](https://www.mongodb.com/products/compass) is a GUI for interacting with MongoDB databases.

- **Node.js / Other Required Software**:  
  If your project involves Node.js, ensure you have Node.js installed:
  - [Download Node.js](https://nodejs.org/)

## Step 1: Install MongoDB

Follow the instructions below based on your operating system.

### MongoDB Installation for macOS

1. **Install Homebrew (if you haven't already)**  
   Open the terminal and run:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install MongoDB**  
   After Homebrew is installed, use it to install MongoDB:
   ```bash
   brew tap mongodb/brew
   brew install mongodb-community@5.0
   ```

3. **Start MongoDB**  
   To start MongoDB as a service:
   ```bash
   brew services start mongodb/brew/mongodb-community
   ```

### MongoDB Installation for Windows

1. **Download MongoDB**  
   Go to [MongoDB's Windows download page](https://www.mongodb.com/try/download/community) and download the appropriate version.

2. **Install MongoDB**  
   Follow the installation steps in the MongoDB installation guide for Windows.

3. **Start MongoDB**  
   After installation, start MongoDB by opening a command prompt and running:
   ```bash
   mongod
   ```

### MongoDB Installation for Linux

1. **Install MongoDB**  
   Use your Linux package manager to install MongoDB. For Ubuntu, the commands are:
   ```bash
   sudo apt update
   sudo apt install -y mongodb
   ```

2. **Start MongoDB**  
   To start MongoDB as a service:
   ```bash
   sudo service mongodb start
   ```

## Step 2: Verify MongoDB Installation

1. Open a terminal and run:
   ```bash
   mongo --version
   ```

   You should see the version of MongoDB installed.

2. To connect to the MongoDB server, run:
   ```bash
   mongo
   ```

   This opens the MongoDB shell. If you see the `>`, you're connected to MongoDB successfully.

## Step 3: Create a Database

To create a new database, follow these steps:

1. Open the MongoDB shell by typing `mongo` in your terminal.

2. Switch to your desired database (if it doesn't exist, MongoDB will create it when you insert data):
   ```bash
   use my_database
   ```

3. Insert a document into a collection:
   ```bash
   db.my_collection.insertOne({ name: "Sample", value: 42 })
   ```

4. To verify the insertion, you can query the collection:
   ```bash
   db.my_collection.find()
   ```

## Step 4: Set Up Database Schema (Optional)
### Example Schema with Mongoose (for Node.js):

1. **Install Mongoose**:
   If you're using Node.js, first install Mongoose by running:
   ```bash
   npm install mongoose
   ```

2. **Create a Mongoose Model**:
   Create a `models` directory and inside it, create a `User.js` file:
   ```js
   const mongoose = require('mongoose');

   const userSchema = new mongoose.Schema({
     name: {
       type: String,
       required: true,
     },
     age: {
       type: Number,
       required: true,
     },
   });

   const User = mongoose.model('User', userSchema);

   module.exports = User;
   ```

3. **Connect to MongoDB with Mongoose**:
   In your app's entry point (e.g., `app.js`), connect to MongoDB:
   ```js
   const mongoose = require('mongoose');

   mongoose.connect('mongodb://localhost/my_database', {
     useNewUrlParser: true,
     useUnifiedTopology: true,
   })
   .then(() => {
     console.log('Connected to MongoDB');
   })
   .catch((err) => {
     console.error('MongoDB connection error:', err);
   });
   ```

4. **Use the Model**:
   In your application, use the `User` model to interact with the database:
   ```js
   const User = require('./models/User');

   const createUser = async () => {
     const user = new User({
       name: 'John Doe',
       age: 30,
     });
     await user.save();
     console.log('User Created:', user);
   };

   createUser();
   ```

## Step 5: Running Your Application

Once MongoDB is running and your application is configured to use the database, you can start your application.

1. **Node.js Example**:  
   If your project uses Node.js, run:
   ```bash
   npm start
   ```

2. **Python Example (using PyMongo)**:
   If you are using Python, install the `pymongo` package:
   ```bash
   pip install pymongo
   ```

   Then use it in your Python script:
   ```python
   from pymongo import MongoClient

   client = MongoClient("mongodb://localhost:27017/")
   db = client.my_database
   collection = db.my_collection

   collection.insert_one({"name": "Sample", "value": 42})
   ```

## Step 6: Accessing MongoDB with MongoDB Compass (Optional)

1. Download and install MongoDB Compass.
2. Open MongoDB Compass and connect to the database using the connection string:  
   `mongodb://localhost:27017`

## Troubleshooting

- **MongoDB not starting**:  
  Make sure that no other application is using the default MongoDB port (`27017`). Check if there are any errors in the terminal where MongoDB is running.

- **Database connection issues**:  
  Double-check that MongoDB is running and ensure your connection string is correct. Also, verify that the MongoDB server is not behind a firewall if you're trying to connect remotely.

## Additional Resources

- [MongoDB Documentation](https://www.mongodb.com/docs/)
- [Mongoose Documentation](https://mongoosejs.com/docs/)

---
