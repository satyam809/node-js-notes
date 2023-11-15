Common security vulnerabilities in Node.js applications include:

1. **Injection Attacks (e.g., SQL Injection):**
   - **Mitigation:** Use parameterized queries or prepared statements to sanitize user inputs.
   - **Example:** Without mitigation:
     ```javascript
     const userInput = req.query.username;
     const sql = `SELECT * FROM users WHERE username = '${userInput}'`;
     db.query(sql, (err, result) => {
       // SQL injection risk
     });
     ```
     With mitigation using parameterized query (using `mysql` library):
     ```javascript
     const userInput = req.query.username;
     const sql = 'SELECT * FROM users WHERE username = ?';
     db.query(sql, [userInput], (err, result) => {
       // Injection risk mitigated
     });
     ```

2. **Cross-Site Scripting (XSS):**
   - **Mitigation:** Sanitize user-generated content and use security libraries like `helmet`.
   - **Example:** Without mitigation:
     ```javascript
     const userInput = req.body.comment;
     const response = `<div>${userInput}</div>`;
     res.send(response);
     ```
     With mitigation using `helmet` to set proper HTTP headers:
     ```javascript
     const helmet = require('helmet');
     app.use(helmet());
     ```

3. **Insecure Dependencies (e.g., outdated packages):**
   - **Mitigation:** Regularly update dependencies and use tools like Snyk for vulnerability scanning.
   - **Example:** In your `package.json`, ensure dependencies are up-to-date:
     ```json
     "dependencies": {
       "express": "^4.17.1",
       "lodash": "^4.17.21"
     }
     ```

4. **Inadequate Authentication and Authorization:**
   - **Mitigation:** Implement strong authentication mechanisms and role-based access control.
   - **Example:** Using Passport.js for authentication and JWT for authorization:
     ```javascript
     const passport = require('passport');
     const JwtStrategy = require('passport-jwt').Strategy;
     const ExtractJwt = require('passport-jwt').ExtractJwt;
     
     passport.use(new JwtStrategy({
       jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
       secretOrKey: 'your-secret-key'
     }, (jwtPayload, done) => {
       // Verify user's authorization here
       // Example: Check user role and permissions
       if (jwtPayload.role === 'admin') {
         return done(null, jwtPayload);
       } else {
         return done(null, false);
       }
     }));
     ```

5. **Denial of Service (DoS) Attacks:**
   - **Mitigation:** Implement rate limiting, request validation, and use tools like `express-rate-limit`.
   - **Example:** Applying rate limiting using `express-rate-limit`:
     ```javascript
     const rateLimit = require('express-rate-limit');
     
     const limiter = rateLimit({
       windowMs: 15 * 60 * 1000, // 15 minutes
       max: 100 // Limit each IP to 100 requests per windowMs
     });
     
     app.use(limiter);
     ```

Mitigating these vulnerabilities is crucial to ensure the security of Node.js applications. Regularly updating dependencies, following best practices, and using security libraries can help protect your application from common threats.

Sources:
1. [Node.js Security: Top Risks and 5 Critical Best Practices - Aqua](https://www.aquasec.com/cloud-native-academy/application-security/node-js-security/)
2. [Top 10 Node.js Security Best Practices](https://snyk.io/learn/nodejs-security-best-practice/)
3. [Top 15 Best Practices for NodeJS Security Issues Mitigation](https://anywhere.epam.com/business/node-js-security-best-practices)
4. [Top 20 Node.js Security Best Practices: Potential Risks and ...](https://www.simform.com/blog/nodejs-security/)
5. [NodeJS Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html)
6. [Node.js Security Vulnerabilities and How to Mitigate Them](https://systemweakness.com/fortifying-node-js-applications-mitigating-security-vulnerabilities-for-a-robust-defense-5e8361f8fbc8)