Unit testing in Node.js is a crucial practice to ensure the individual units or components of your code (such as functions or methods) work correctly in isolation. In this step-by-step example, we'll set up a simple unit test using the popular testing framework Mocha and an assertion library called Chai.

**Step 1: Set Up a Node.js Project**

First, create a new directory for your Node.js project and initialize it with `npm`:

```bash
mkdir node-unit-testing-example
cd node-unit-testing-example
npm init -y
```

**Step 2: Install Testing Dependencies**

Install Mocha and Chai as development dependencies:

```bash
npm install mocha chai --save-dev
```

**Step 3: Create a Module to Test**

Let's create a simple module that we want to test. Create a file named `math.js` in your project directory:

```javascript
// math.js

module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b,
};
```

**Step 4: Write Unit Tests**

Now, create a directory named `test` in your project directory to store your test files. Inside the `test` directory, create a test file named `math.test.js`:

```javascript
// test/math.test.js

const math = require('../math'); // Import the module to be tested
const chai = require('chai');
const expect = chai.expect;

describe('Math Module', () => {
  it('should add two numbers correctly', () => {
    const result = math.add(2, 3);
    expect(result).to.equal(5);
  });

  it('should subtract two numbers correctly', () => {
    const result = math.subtract(5, 3);
    expect(result).to.equal(2);
  });
});
```

In this test file, we import the `math` module and write test cases using Mocha's `describe` and `it` functions along with Chai's `expect` for assertions.

**Step 5: Configure Test Script**

In your `package.json` file, add a test script that runs Mocha:

```json
"scripts": {
  "test": "mocha"
}
```

**Step 6: Run the Tests**

Now, you can run your tests using the following command:

```bash
npm test
```

Mocha will discover and execute the test cases defined in your `math.test.js` file. If all tests pass, you will see an output indicating that the tests ran successfully.

**Step 7: Review Test Results**

The test results will be displayed in your terminal, showing the number of passing and failing tests, as well as any errors or failures.

That's it! You've set up a basic unit testing framework for a Node.js module. You can extend this example to include more test cases and cover other parts of your codebase. Unit testing is an essential practice for maintaining code quality and catching bugs early in the development process.