# Cypress Architecture 
Cypress is a unique end to end testing framework that offers a modern and friendly approach to testing applications. Understanding its architecture is crucial to leveraging its full potential. In this explanation, we will break down the key components of cypress architecture and how they work together to provide a seamless testing experience. 

# Key components
**- Cypress Test Runner**
**- Node.js Backend**
**- Cpress CLI**
**- Browser Execution**
**- Test Code and Application Code**

# Cypress Test Runner:
The Cypress test runner is the core of the cypress architecture. It provides as interactive interface where you can write, run and debug your tests in real time. The test runner open your application in a browser and allows you to interact with it just like a user would. <Read from video file>

# Node.js Backend:
Cypress is build on Node.js, where serves as the backend for running and managing tests. The node.js backend handles tasks like <Read from video file>.
This separation allows cypress to take advantage of Node.js capabilities while ensuring tests run efficiently.

# Cypress CLI:
The cypress command line interface (CLI) is the tool you use to interact with cypress from your terminal. It allows you to <Read from video file> <Sow the example>
The CLI is an essential tool for integrating cypress into your test development and workflow.

**1. Browser Execution**
    Cypress runs tests directly in the browser providing a true end to end testing environment.
    This approach has several advantages:
    <Read from video file>
    <Show the example>

**2. Test Code and Application Code**
    In cypress, your test code runs alongside your application code in the same execution loop. This unique approach allows for
        **1.    <Show the heading in video file and read from here>  Synchronous execution**
        Unlike traditional selenium based frameworks that use asynchronous execution, cypress runs synchronously making it easier to write and understand tests.
        **2.    <Show the heading in video file and read from here>  Access to application internals**
            Cypress can access and manipulate the state of your application, providing powerful capabilities for testing complex scenarios. I have not tested this feature but seems its gonna be a time saving feature especially when you are testing a front heavy application.
            As a tester, I always profer to test in the same condition as it was delivered to us then only we can certify the quality else quality go for a toss. But if you are testing a frontend heavy application and showing the information from multiple apis in the UI and if one or two api is still under development, we can stubb those api requests and test rest of the apis. This way test won't get halted. (Stubbing is mainly used to replicate the behaviour of an API in a controlled manner with predefined responses which allows to focus on testing the integration and functionality of the code without worrying about external dependencies.)
        **3.    <Show the heading in video file and read from here> Automatic waiting>**
            Cypress automatically waits for elements to appear reducing the need for hardcoding the waits and timeouts.
        
        When using Selenium for web automation, waiting for elements to load on a page can be tricky. 
        Though we have Implicit Waits and Explicit Waits, test cases are often faile with these reasons
            Element Not Found Error
            Timeouts
            Stale Element Exception
        And hence we end up retrying a test case for N retries(may be 3) so to avoid flacky failure. 

        In other hand, cypress waiting mechanism is not like selenium <Show the cypress architecture and explain this context.>


**3. How it all comes together**
    When you run a Cypress test, here's what happens under the hood:
        <Show the video file for pointers and explain from this file.>
        **Initialization :** The Cypress CLI initializes the Test Runner, which opens the specified browser and loads your application.
        **Test Execution :** The test code is executed in the browser's context, interacting with the application as a user would.
        **Node.js Integration :** The Node.js backend handles any necessary server-side tasks, such as stubbing network requests or accessing the file system.
        **Real-time Feedback :** The Test Runner provides real-time feedback, displaying the results of each test step, and allowing you to debug issues on the spot.


# How Cypress Commands Are Added to the Queue
Cypress commands are added to the command queue in a way that ensures they are executed sequentially and synchronously. This process is fundamental to how Cypress handles test execution, providing a reliable and intuitive testing experience. Here's a detailed explanation of how Cypress commands are added to the queue.

**1. Writing Cypress Commands**

When you write Cypress tests, you typically chain commands together. Each command you write gets added to an internal queue managed by Cypress.

- **Example Test**:
  ```javascript
  cy.visit('/login');
  cy.get('input[name="username"]').type('myUsername');
  cy.get('input[name="password"]').type('myPassword');
  cy.get('button[type="submit"]').click();
  ```

**2. Command Chaining**

Cypress commands are designed to be chainable. Each command returns a `cy` object, allowing you to chain the next command.

- **Chaining Example:**
  ```javascript
  cy.visit('/login')
    .get('input[name="username"]').type('myUsername')
    .get('input[name="password"]').type('myPassword')
    .get('button[type="submit"]').click();
  ```

**3. Queuing Mechanism**

When Cypress encounters a command, it doesn't execute it immediately. Instead, it adds the command to an internal queue. This queuing mechanism ensures that commands are executed in the exact order they are written, one after another.

- **Command Queue**:
  - `cy.visit('/login')` is added to the queue.
  - `cy.get('input[name="username"]').type('myUsername')` is added to the queue.
  - `cy.get('input[name="password"]').type('myPassword')` is added to the queue.
  - `cy.get('button[type="submit"]').click()` is added to the queue.

**4. Execution Loop**

Cypress has an execution loop that processes the command queue. The loop ensures that each command completes before the next one begins.

- **Execution Flow**:
  - **Start**: Cypress starts processing the first command in the queue.
  - **Wait**: If a command requires waiting (e.g., for an element to appear), Cypress automatically waits.
  - **Execute**: Once the condition is met, Cypress executes the command.
  - **Next**: Cypress moves to the next command in the queue and repeats the process.

**5. Command Execution Example**

Here’s a step-by-step breakdown of how the commands are added to the queue and executed:

1. **Visit Command**:
   ```javascript
   cy.visit('/login');
   ```
   - Added to the queue.
   - Execution starts, browser navigates to the login page.
   - Cypress waits for the page to load before proceeding.

2. **Get Username Input**:
   ```javascript
   cy.get('input[name="username"]').type('myUsername');
   ```
   - `cy.get('input[name="username"]')` is added to the queue.
   - Cypress waits for the element to appear.
   - Element found, command is executed.
   - `type('myUsername')` is added to the queue.
   - Cypress types the username into the input field.

3. **Get Password Input**:
   ```javascript
   cy.get('input[name="password"]').type('myPassword');
   ```
   - `cy.get('input[name="password"]')` is added to the queue.
   - Cypress waits for the element to appear.
   - Element found, command is executed.
   - `type('myPassword')` is added to the queue.
   - Cypress types the password into the input field.

4. **Click Submit Button**:
   ```javascript
   cy.get('button[type="submit"]').click();
   ```
   - `cy.get('button[type="submit"]')` is added to the queue.
   - Cypress waits for the button to appear.
   - Button found, command is executed.
   - `click()` is added to the queue.
   - Cypress clicks the submit button.


# Conclusion:
Cypress architecture is designed to provide a seamless and efficient testing experience by integrtingtightly with the browser and leveraging the power of Node.js. This architecture enables cypress to offer features like real time reloads, automatic waiting for UI elements and page navigations, debugging capabilities making it a powerful tool for modern web applicaiton automation. Understanding this architecture will help you make the most out of cyupress and write reliable, maintainable tests for your application.