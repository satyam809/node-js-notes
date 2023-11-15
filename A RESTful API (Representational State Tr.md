A RESTful API (Representational State Transfer) is a web service architectural style that uses a set of constraints and principles for designing networked applications. It is based on HTTP methods and uses standard HTTP status codes to perform CRUD (Create, Read, Update, Delete) operations on resources. Here's an explanation with an example in Node.js:

**Creating a RESTful API in Node.js:**

1. **Initialize a Node.js Project:**
   Start by creating a new Node.js project and installing the necessary dependencies like `express` and `body-parser` using npm or yarn.

2. **Set Up an Express Server:**
   Create an Express server to handle HTTP requests.

   ```javascript
   const express = require('express');
   const bodyParser = require('body-parser');
   const app = express();
   const port = 3000;

   app.use(bodyParser.json());

   // Define your routes and handlers here

   app.listen(port, () => {
     console.log(`Server is running on port ${port}`);
   });
   ```

3. **Define Routes and Handlers:**
   Create routes for different resources and define handlers to handle CRUD operations. Here's an example for a simple RESTful API with a "users" resource:

   ```javascript
   let users = [
     { id: 1, name: 'Alice' },
     { id: 2, name: 'Bob' },
   ];

   // GET all users
   app.get('/users', (req, res) => {
     res.json(users);
   });

   // GET a specific user by ID
   app.get('/users/:id', (req, res) => {
     const userId = parseInt(req.params.id);
     const user = users.find((u) => u.id === userId);
     if (user) {
       res.json(user);
     } else {
       res.status(404).json({ message: 'User not found' });
     }
   });

   // POST - Create a new user
   app.post('/users', (req, res) => {
     const newUser = req.body;
     users.push(newUser);
     res.status(201).json(newUser);
   });

   // PUT - Update a user by ID
   app.put('/users/:id', (req, res) => {
     const userId = parseInt(req.params.id);
     const updatedUser = req.body;
     const index = users.findIndex((u) => u.id === userId);
     if (index !== -1) {
       users[index] = updatedUser;
       res.json(updatedUser);
     } else {
       res.status(404).json({ message: 'User not found' });
     }
   });

   // DELETE - Delete a user by ID
   app.delete('/users/:id', (req, res) => {
     const userId = parseInt(req.params.id);
     const index = users.findIndex((u) => u.id === userId);
     if (index !== -1) {
       users.splice(index, 1);
       res.json({ message: 'User deleted' });
     } else {
       res.status(404).json({ message: 'User not found' });
     }
   });
   ```

4. **Testing the API:**
   You can use tools like Postman or cURL to test your RESTful API by making HTTP requests to the defined endpoints (GET, POST, PUT, DELETE).

This example demonstrates the fundamental principles of RESTful APIs in Node.js, including defining routes for resources, handling different HTTP methods, and using HTTP status codes for responses.