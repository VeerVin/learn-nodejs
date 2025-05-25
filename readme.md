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

**Reading Files:**

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

**Writing Files:**

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

**Appending to Files:**

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

- Blocking: A blocking operation halts the execution of other code until it completes. In synchronous operations, the program executes line by line, and if one line takes a long time, it blocks the execution of subsequent lines. 
- Non-blocking: A non-blocking operation allows the program to continue executing other tasks while waiting for the operation to complete. Node.js leverages asynchronous, non-blocking I/O operations to prevent blocking the main thread. 

**Asynchronous Nature**

- Node.js is inherently asynchronous, meaning it doesn't wait for I/O operations (like reading from a file or a network request) to finish before moving on to other tasks. Instead, it uses callbacks, promises, or async/await to handle the results of these operations when they are complete. 
- This approach allows Node.js to handle many concurrent connections efficiently, making it suitable for building high-performance applications. When a long-running operation is initiated, Node.js registers a callback function and continues executing other code. Once the operation completes, the callback is executed, handling the result.

**Example:**

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

### Why Node JS uses callback function?

Callbacks are fundamental to Node.js. Node.js uses an event-driven architecture, where operations that might take time, such as file system access or network requests, don't block the main thread. Instead, Node.js initiates these operations and then continues executing other code. When the operation completes, a callback function is executed to handle the result.

This approach allows Node.js to handle multiple requests concurrently, making it efficient for I/O-bound tasks. Callbacks are used extensively in Node.js APIs, ensuring that the program remains responsive even when dealing with time-consuming operations. They are a core mechanism for managing asynchronous control flow in Node.js applications.

### Node.js Event-Driven Architecture

Node.js is renowned for its non-blocking, asynchronous nature, which is primarily facilitated by its event-driven architecture. This paradigm allows Node.js applications to handle a large number of concurrent connections efficiently without creating a new thread for each connection, unlike traditional multi-threaded servers.

***Core Concepts***
At its heart, the event-driven architecture in Node.js revolves around a few key components:

- Events: These are actions or occurrences that happen in the system, such as a user clicking a button, data arriving from a network request, a file being read, or a timer expiring.

- Event Emitters: These are objects that emit named events. In Node.js, many built-in modules (like http, fs, net) are event emitters, and you can also create custom ones using the EventEmitter class. When an event occurs, the emitter "emits" it.

- Event Listeners (or Handlers): These are functions that "listen" for specific events emitted by an event emitter. When an event is emitted, all registered listeners for that event are executed.

- Event Loop: This is the underlying mechanism that continuously checks for events in the event queue and dispatches them to their respective listeners. It's a single-threaded process that manages all asynchronous operations. While the event loop itself is single-threaded, it offloads I/O operations to the operating system kernel or a thread pool, allowing Node.js to remain non-blocking.

- Non-blocking I/O: When Node.js performs an I/O operation (like reading a file or making a network request), it doesn't wait for the operation to complete. Instead, it sends the request and immediately continues processing other code. Once the I/O operation finishes, it emits an event, and a callback function (the event listener) is put into the event queue to be processed by the event loop.

***How it Works (The Flow)***
Imagine a server handling incoming web requests:

- Request Arrives: An incoming HTTP request (an "event") arrives at the Node.js server.

- Event Emission: The http module (an Event Emitter) emits a 'request' event.

- Listener Activation: The application's code has an event listener (a callback function) registered for the 'request' event. This listener is triggered.

- Asynchronous Operation (if any): Inside the listener, if there's an I/O operation (e.g., querying a database, reading a file), Node.js hands off this task to the underlying system (via libuv, which manages a thread pool for heavy lifting) and immediately returns to the event loop. It doesn't wait.

- Event Loop Continues: The event loop is now free to process other incoming requests or other events in the queue.

- I/O Completion & Callback: Once the database query or file read completes, it signals Node.js. The associated callback function (the "continuation" of the original request) is placed back into the event queue.

- Callback Execution: When the event loop is free, it picks up this callback from the queue and executes it, allowing the server to send the response back to the client.

This continuous cycle allows Node.js to handle many operations concurrently without blocking the main thread.

***Diagram of Node.js Event-Driven Architecture***
![Event driven architecture diagaram](./images/event-driven-architecture.png)

***Explanation of the Diagram:***

- User Interaction / External Input: Represents anything that triggers an event (e.g., a new HTTP request, a user clicking a button in a client-side app that interacts with Node.js, a file operation starting).

- Event Emitter: The part of Node.js or your application that detects the occurrence of an event and "emits" it.

- Node.js Event Loop: The central orchestrator. It's constantly running, checking if there are any events to process. When it encounters an I/O operation, it hands it off and doesn't wait.

- I/O Completion: When an asynchronous operation (like a database query or file read) finishes, it signals the Node.js environment.

- Event Queue: When an I/O operation completes, its associated callback function is placed into this queue, waiting for the Event Loop to pick it up. Similarly, direct events emitted by an Event Emitter also lead to their listeners being placed here.

- Event Listener (Callback Function): The actual code that gets executed when the Event Loop processes an event from the queue.

***Benefits of Event-Driven Architecture in Node.js***
- Scalability: Can handle a large number of concurrent connections with minimal overhead, making it ideal for real-time applications, APIs, and microservices.

- Performance: Non-blocking I/O ensures that the server doesn't sit idle waiting for slow operations, maximizing CPU utilization.

- Simplicity: The asynchronous model with callbacks/promises/async-await simplifies handling concurrent operations compared to complex thread management.

- Efficiency: Uses fewer system resources (memory, CPU) per connection than traditional blocking I/O models.

In essence, Node.js's event-driven architecture is what enables it to be so efficient and performant for I/O-bound applications.


