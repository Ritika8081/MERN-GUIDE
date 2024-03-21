# What is the MERN stack?

The phrase MERN stack comprises the following technologies that allow for faster application development:

- [MongoDB](https://www.mongodb.com/): A cross-platform document-oriented database program
- [Express.js](https://expressjs.com/): A web application framework for Node.js
- [React](https://reactjs.org/): JavaScript library for building user interfaces
- [Node.js](https://nodejs.org/en/): An open source, cross-platform, JavaScript runtime environment that executes JavaScript code outside of a browser
  
- MongoDB, Express.js, and Node.js help you build the backend of an application, while React powers the frontend. 
  
- Learning the MERN stack will help you become a full-stack developer.
- 
  ## Server setup with Express.js and Node.js
  
  This demo is designed to highlight the MERN setup. The objective is to develop a simple project with the best possible structure so that you can use it as a boilerplate and elevate your MERN stack projects to meet industry standards.
  
 To begin our MERN stack tutorial, how to set up a server with Express.js and Node.js.


  # npm package initialization
 To create a project folder, enter the folder through the terminal, then run $ npm init. It will then ask you some questions about the package name, version, entry point, and more.
 
 This will create a file named package.json. Alternatively, you can append a -y flag to the command, which will instruct the CLI to use the default configurations:
```
   npm init -y
  ```
  # Installing the dependencies
- Next, we’ll add some dependencies with $ npm i express mongoose body-parser .
- body-parser: Allows us to get the data throughout the request
- express: Is our main framework
- mongoose: Is used to connect and interact with MongoDB

Now, we’ll add [nodemon](https://nodemon.io/) as a dev dependency. 
`
npm i -D nodemon
`
 To use nodemon, add "app": "nodemon app.js" to your scripts tag under the package.json file.
 nodemon is a utility that will monitor any changes in your source . The app.js is the entry point for the application. It is also important to define a start script here with "start": "node app.js".
  
  # Setting the entry point
 Now, create a file named app.js for our entry point. You can create this from the terminal with the $ touch app.js command.
  

`
  // app.js
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello world!'));
 const port = process.env.PORT || 8082;
app.listen(port, () => console.log(Server running "));
`

 After that, run the $ node app command. You will see Server running on port 8082. You can also check it from the browser by opening the browser and entering http://localhost:8082.
 At this point, if we change anything, we’ll need to restart the server manually. But, if we set up nodemon, then we don’t have to restart it every time. nodemon will watch if there is any change and restart the server automatically.
  
 So, what you need to do for that is a little change to the scripts in our package.json file. See below:
  
  `
  // package.json
  {
  "name": "mern\_a\_to\_z",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "start": "node app.js",
  "app": "nodemon app.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
 "body-parser": "^1.20.2",
  "config": "^3.3.9",
  "cors": "^2.8.5",
  "express": "^4.18.2",
  "mongoose": "^8.0.2",
  "nodemon": "^3.0.2"
  }
  } 
  `
  
 Now, you can run your project using the $ npm runapp command. If you get any error at this point, run the commands below:
 
  `
 $ npm install
 $ npm run app
 `
  # Database setup with MongoDB
  
- MongoDB provides a multi-cloud database service known as Atlas, which simplifies the process of deploying and managing MongoDB databases. We will use Atlas to create the database for our MERN application.


Optimizing the database performance is essential, especially when scaling your application and for large-scale MERN applications, as this improves the performance of your application. MongoDB provides various methods to achieve this, including but not limited to:

- Indexes: Implementing appropriate indexes on frequently queried fields can significantly enhance query performance
- Sharding: Sharding distributes data across multiple servers, thereby improving scalability
- Caching strategies: Utilizing caching mechanisms like Redis or in-memory caching can reduce database load and enhance overall application performance
- Query optimization: Crafting efficient queries and leveraging MongoDB’s query planner to analyze and improve query execution plans
- Document structure: Designing an optimal document structure by embedding related data and avoiding complex joins can improve performance
- **Adding the database to our project**
- Now that we have a database set up, we can go ahead and connect it to our project.
- Inside the project folder, create another folder named config, and add a db.js

  `
// db.js
 const mongoose = require("mongoose");
 const db =
"mongodb+srv://logrocket:<password>@cluster1.dydb2rf.mongodb.net/?retryWrites=t rue&w=majority";
 /\* Replace <password> with your database password \*/
mongoose.set("strictQuery", true, "useNewUrlParser", true);
const connectDB = async () => {
 try {
 await mongoose.connect(db);
 console.log("MongoDB is Connected...");
  } catch (err) {
  console.error(err.message);
 process.exit(1);
 }
 };
  module.exports = connectDB;
  `
 You must replace the string in the code above with the one you copied from your database in the previous section, as well as the placeholder with the user password you copied from the dashboard.
 We need a little change in our app.js file to connect to the database. Update your app.js
`
  // app.js
 const express = require('express');
 const connectDB = require('./config/db');
 const app = express();
`
`
// Connect Database
connectDB();
app.get('/', (req, res) => res.send('Hello world!'));
const port = process.env.PORT || 8082;
app.listen(port, () => console.log(`Server running on port ${port}`));
`
- Now, you can run the project using the $ npm run app command.
- Great! So far, we are on the right track, and our database is successfully connected. Now, time to complete the route setup.
- 
  ## Building RESTful APIs with the MERN stack
  
 To get started, create a folder named routes. In it, create another folder named api, which will hold all our APIs. Inside the api folder, create a file named books.js. We will create some APIs here to show how it works in a moment.
 



