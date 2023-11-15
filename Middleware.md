Middleware in Node.js is a fundamental concept used in web application development to perform tasks or operations in between receiving an HTTP request and sending an HTTP response. It is essentially a series of functions that can be executed in a specific order to process, modify, or enhance the request or response objects. Middleware functions have access to these objects and can manipulate them as needed.

Here's an explanation of middleware in Node.js with examples:

1. **Express.js Middleware**:
   Express.js is a popular Node.js framework that simplifies building web applications. Middleware is extensively used in Express to handle various tasks like authentication, logging, parsing requests, and more.

   Example of using middleware in Express.js:

   ```javascript
   const express = require('express');
   const app = express();

   // Middleware function to log requests
   app.use((req, res, next) => {
     console.log(`Received request for ${req.url}`);
     next(); // Call next to continue processing
   });

   // Route handler
   app.get('/', (req, res) => {
     res.send('Hello, World!');
   });

   app.listen(3000, () => {
     console.log('Server started on port 3000');
   });
   ```

   In this example, `app.use` is used to register a middleware function that logs each incoming request. The `next` function is called to pass control to the next middleware in the chain.

2. **Custom Middleware**:
   You can create your own custom middleware functions to perform specific tasks. For example, you might create middleware to check if a user is authenticated before allowing access to certain routes.

   Example of custom middleware in Express.js:

   ```javascript
   // Custom middleware to check authentication
   const checkAuth = (req, res, next) => {
     if (req.isAuthenticated()) {
       return next(); // User is authenticated, continue
     }
     res.status(401).send('Unauthorized'); // User is not authenticated
   };

   // Protected route
   app.get('/dashboard', checkAuth, (req, res) => {
     res.send('Welcome to the dashboard!');
   });
   ```

   In this example, `checkAuth` is a custom middleware that checks if the user is authenticated before allowing access to the "/dashboard" route.

3. **Third-party Middleware**:
   Express.js allows you to use third-party middleware packages to add functionality to your application easily. Common third-party middleware includes `body-parser` for parsing request bodies, `cors` for handling Cross-Origin Resource Sharing, and `morgan` for logging.

   Example of using `body-parser` middleware:

   ```javascript
   const express = require('express');
   const bodyParser = require('body-parser');
   const app = express();

   // Parse JSON requests
   app.use(bodyParser.json());

   app.post('/api/data', (req, res) => {
     const data = req.body;
     // Process data and send a response
   });
   ```

   In this example, the `body-parser` middleware is used to parse incoming JSON requests.

Middleware in Node.js and Express allows you to modularize and organize your code effectively by breaking down the request/response handling process into smaller, reusable functions. Each middleware function can perform a specific task, making your code cleaner and more maintainable.