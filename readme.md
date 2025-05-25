# What is Node js
Node.js is a runtime environment that allows developers to execute JavaScript code outside of a web browser. It is built on the V8 JavaScript engine, the same engine that powers Google Chrome, enabling high performance. Node.js is open-source, cross-platform, and designed for building scalable network applications. It excels in handling concurrent operations efficiently through its non-blocking, event-driven architecture. 

Node.js operates on a single thread, utilizing an event loop to manage multiple tasks concurrently. This approach allows it to handle numerous connections with minimal overhead, making it suitable for real-time applications and I/O-intensive tasks. It is commonly used for server-side development, creating APIs, and building command-line tools.

### Node JS Pros
- Single-threaded, based on event drive, non blocking I/O model
- Perefect for building fast and scalable data-intensive apps.

### Use Node JS
- Api with Database behind it
- Data stream (think Youtube)
- Real time chat application
- server side web application

### Don't Use Node JS
- Applciations with heavy server side processing. Node.js is single-threaded by default and designed for I/O-bound operations. Heavy CPU tasks (e.g., image/video processing, data crunching, or complex algorithms) can block the event loop and degrade performance.
- Applications with Blocking Code or Heavy Threading Needs. If your application relies on synchronous operations or needs multi-threading (e.g., scientific computing, batch jobs), Node.js isn’t ideal out of the box.
- While Node.js supports SQL databases, it's more naturally suited for NoSQL and event-driven systems. Handling complex SQL queries and transactions isn't Node’s strength.

## What is Node JS REPL?
The Node.js REPL (Read-Eval-Print Loop) is an interactive shell that allows the execution of JavaScript code within a Node.js environment. It is a tool for testing, debugging, and experimenting with JavaScript code. When the node command is executed without any arguments, it initiates a REPL session, presenting a prompt where JavaScript code can be entered. The REPL then reads the input, evaluates it, prints the result, and loops back to await further input. This cycle continues until the user exits the session, typically by pressing.

Enter node in terminal and you can start using it.

Special commands available in the REPL include: 
- .help: Displays a list of available commands.
- .break: Cancels the current multi-line expression.
- .clear: Resets the REPL context and clears multi-line input.
- .exit: Closes the I/O stream and exits the REPL.
- .save: Saves the current REPL session to a file.
- .load: Loads a file into the current REPL session.

## What is Module in Node JS?

In Node.js, a module is a self-contained unit of code that encapsulates related functions, classes, or data. Modules enable developers to organize code into reusable components, promoting modularity, maintainability, and code reuse. Node.js employs the CommonJS module system by default, although it also supports ECMAScript (ES) modules.

### There are three main types of modules in Node.js: 
- Built-in modules: These modules are bundled with Node.js and provide core functionalities, such as file system operations (fs), HTTP requests (http), and path manipulation (path).

- Local modules: These are custom modules created by developers within their applications. They allow for the organization of application-specific logic into separate files.

- Third-party modules: These modules are external packages installed using npm (Node Package Manager). They provide a wide range of functionalities and can be easily integrated into Node.js applications.

Example of using the local module in another file (app.js):
const myModule = require('./myModule');
const fs = require('fs');

## What does fs module do in Node JS?

The fs module in Node.js provides an API for interacting with the file system. It enables operations such as reading, writing, creating, updating, deleting, and renaming files and directories. The module offers both synchronous and asynchronous methods for these operations. Asynchronous methods are non-blocking, allowing the application to continue executing other tasks while file operations are in progress. Synchronous methods, on the other hand, block execution until the operation is complete. [1]  
Commonly used methods include: [2]  

- fs.readFile(): Reads the content of a file. 
- fs.writeFile(): Writes data to a file, replacing the file if it exists. 
- fs.appendFile(): Appends data to a file. 
- fs.unlink(): Deletes a file. 
- fs.rename(): Renames a file. 
- fs.mkdir(): Creates a directory. 
- fs.rmdir(): Deletes a directory. 
- fs.readdir(): Reads the contents of a directory. 
- fs.stat(): Retrieves information about a file or directory, such as its size and type. 

The fs module is a core module in Node.js and does not require installation. It is imported using the require('fs') statement.

Here is how to read and write files in Node.js using the fs (file system) module:

Reading Files:

```javascript
const fs = require('fs');

// Asynchronous read
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error("An error occurred:", err);
    return;
  }
  console.log(data);
});

// Synchronous read
try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error("An error occurred:", err);
}
```

Writing Files:

```javascript
const fs = require('fs');

// Asynchronous write
const content = 'Hello, Node.js!';
fs.writeFile('example.txt', content, 'utf8', err => {
  if (err) {
    console.error("An error occurred:", err);
    return;
  }
  console.log("File written successfully");
});

// Synchronous write
try {
  fs.writeFileSync('example.txt', content, 'utf8');
  console.log("File written successfully");
} catch (err) {
  console.error("An error occurred:", err);
}
```

Appending to Files:

```javascript
const fs = require('fs');

// Asynchronous append
const content = '\nThis line is appended.';
fs.appendFile('example.txt', content, 'utf8', err => {
    if (err) {
        console.error("An error occurred:", err);
        return;
    }
    console.log("File appended successfully");
});

// Synchronous append
try {
    fs.appendFileSync('example.txt', content, 'utf8');
    console.log("File appended successfully");
} catch (err) {
    console.error("An error occurred:", err);
}
```
## Blocking and Non-blocking, Asynchronous nature of Node js

Node.js, designed for scalability and high performance, operates on a single-threaded, non-blocking, and asynchronous architecture. This approach allows it to handle multiple concurrent requests efficiently. 
Blocking vs. Non-blocking 

• Blocking: A blocking operation halts the execution of other code until it completes. In synchronous operations, the program executes line by line, and if one line takes a long time, it blocks the execution of subsequent lines. 
• Non-blocking: A non-blocking operation allows the program to continue executing other tasks while waiting for the operation to complete. Node.js leverages asynchronous, non-blocking I/O operations to prevent blocking the main thread. 

Asynchronous Nature 

• Node.js is inherently asynchronous, meaning it doesn't wait for I/O operations (like reading from a file or a network request) to finish before moving on to other tasks. Instead, it uses callbacks, promises, or async/await to handle the results of these operations when they are complete. 
• This approach allows Node.js to handle many concurrent connections efficiently, making it suitable for building high-performance applications. When a long-running operation is initiated, Node.js registers a callback function and continues executing other code. Once the operation completes, the callback is executed, handling the result. [1]  

Example:

```javascript
const fs = require('fs');

// Non-blocking (asynchronous) file read
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return;
  }
  console.log("File content:", data);
});

console.log("This message is printed before the file content.");

// Blocking (synchronous) file read
try {
  const data = fs.readFileSync('file.txt', 'utf8');
  console.log("File content (synchronous):", data);
} catch (err) {
  console.error("Error reading file (synchronous):", err);
}

console.log("This message is printed after the synchronous file read.");
```

In the example above, the asynchronous readFile function does not block the execution of the subsequent console.log statement. The "This message is printed before the file content." line will be printed first. Once the file reading is complete, the callback function is executed, and the file content is printed. Conversely, readFileSync will block the execution until the file is read, ensuring that "This message is printed after the synchronous file read." is printed only after the file content.


