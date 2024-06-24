# **_Key Components of Cypress Architecture_**
- **Cypress Test Runner**
- **Node.js Backend**
- **Cypress CLI**
- **Browser Execution**
- **Test Code and Application Code**


# _Cypress Test Runner_
- **Real-time reloads**: 
		Tests are re-executed automatically when code changes.
- **Time-travel**: 
		View snapshots of your application at each step of your tests.
- **Detailed logs**: 
		See detailed logs and error messages to debug your tests effectively

# _Node.js Backend_
	- Executing the Cypress CLI commands.
	- Managing the communication between the Test Runner and the browser.

# _Cypress CLI_
	- Install Cypress and manage its versions.
	- Open the Cypress Test Runner.
	- Run tests in headless mode for CI/CD integration.
	- Configure various settings for your test environment.

# _Browser Execution Show the architecture diagram_
	- Cypress can trigger native events like clicks, typing and scrolling, ensuring your tests interact with the application as a user would.
	- Each test runs in a clean state, isolated from other tests, which helps prevent flaky tests and ensures consistent results.
	- Running tests directly in the browser allows for fast execution and immediate feedback.

# _Test Code and Application Code_
	- Synchronous execution
	- Access to application internals
	- Automatic waiting

# _How It All Comes Together_
	- Initialization
	- Test Execution
	- Node.js Integration
	- Real-time Feedback


# _How Cypress Commands Are Executed_
	- Writing Cypress Commands
```javascript
            cy.visit('/login');
            cy.get('input[name="username"]').type('myUsername');
            cy.get('input[name="password"]').type('myPassword');
            cy.get('button[type="submit"]').click();
```
	- Command Chaining
```javascript
            cy.visit('/login')
            .get('input[name="username"]').type('myUsername')
            .get('input[name="password"]').type('myPassword')
            .get('button[type="submit"]').click();
```
	- Queuing Mechanism
		- `cy.visit('/login')` is added to the queue.
		- `cy.get('input[name="username"]').type('myUsername')` is added to the queue.
		- `cy.get('input[name="password"]').type('myPassword')` is added to the queue.
		- `cy.get('button[type="submit"]').click()` is added to the queue.

	- Execution Loop

	- Command Execution Example
```javascript
	cy.visit('/login'); is added to the queue.
	cy.get('input[name="username"]').type('myUsername'); is added to the queue.
	cy.get('input[name="password"]').type('myPassword'); is added to the queue.
	cy.get('button[type="submit"]').click(); is added to the queue.
```
