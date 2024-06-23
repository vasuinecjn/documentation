Key Components of Cypress Architecture

1. Cypress Test Runner

	- Real-time reloads: Tests are re-executed automatically when code changes.
  	- Time-travel: View snapshots of your application at each step of your tests.
  	- Detailed logs: See detailed logs and error messages to debug your tests effectively

2. Node.js Backend

	- Executing the Cypress CLI commands.
	- Managing the communication between the Test Runner and the browser.

3. Cypress CLI

	- Install Cypress and manage its versions.
	- Open the Cypress Test Runner.
	- Run tests in headless mode for CI/CD integration.
	- Configure various settings for your test environment.

4. Browser Execution <Show the architecture diagram>
	- Cypress can trigger native events like clicks, typing and scrolling, ensuring your tests interact with the application as a user would.
	- Each test runs in a clean state, isolated from other tests, which helps prevent flaky tests and ensures consistent results.
	- Running tests directly in the browser allows for fast execution and immediate feedback.

5. Test Code and Application Code
	- Synchronous execution
	- Access to application internals
	- Automatic waiting


6. How It All Comes Together:

	- Initialization
	- Test Execution
	- Node.js Integration
	- Real-time Feedback


7. How Cypress Commands Are Executed:
	- Writing Cypress Commands
	- Command Chaining
	- Queuing Mechanism
	- Execution Loop
	- Command Execution Example
		```javascript
  			cy.visit('/login'); is added to the queue.
  			cy.get('input[name="username"]').type('myUsername'); is added to the queue.
  			cy.get('input[name="password"]').type('myPassword'); is added to the queue.
  			cy.get('button[type="submit"]').click(); is added to the queue.
  		```
