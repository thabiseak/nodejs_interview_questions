# Introduction to Node JS & Node JS Modules



## Node.js Basics

1. **What is Node.js and what is it used for?**
   - Node.js is a tool that lets you run JavaScript on your server, not just in the browser. It's great for building fast, scalable network applications, like web servers and real-time chat apps.

2. **Explain the main differences between Node.js and traditional web server
environments like Apache or Nginx.**
   - **Node.js**: Uses a single-thread, handles multiple tasks concurrently with non-blocking I/O, written in JavaScript.
   - **Apache/Nginx**: Use multiple threads or processes, each handling a single task, commonly work with languages like PHP, Python, etc.

3. **What is the V8 engine and how does Node.js utilize it?**
   - The V8 engine, made by Google, runs JavaScript fast by turning it into machine code. Node.js uses V8 to run JavaScript on the server side.

4. **Describe the event-driven architecture of Node.js:**
   - Node.js waits for events (like a file read completion) and reacts to them with callbacks, allowing it to handle many operations at once without getting blocked.

5. **What are some common use cases for Node.js?**
   - Real-time chat apps, APIs, single-page applications, server-side rendering, IoT apps, data streaming, and proxies.

6. **How does Node.js handle asynchronous operations?**
   - Node.js uses callbacks, Promises, and async/await to manage operations that take time (like reading files or making network requests) without waiting for them to finish.

7. **What is the purpose of the package.json file in a Node.js project?**
   - It keeps track of project details (like name and version) and lists dependencies, making it easy to share and manage the project.

8. **Explain the role of the Node Package Manager (NPM).**
   - NPM installs and manages packages (libraries or modules) for your Node.js project, helping you add and update dependencies easily.

9. **What is the node_modules folder and why is it important?**
   - This folder contains all the packages your project depends on. Without it, your project won’t run because it won’t find the required libraries.

10. **How to check the version of Node.js and NPM installed on your system?**
    - Use `node -v` to check Node.js version and `npm -v` to check NPM version.

11. **How does Node.js handle concurrency and what are the benefits of this
approach?**
    - Node.js uses a single-threaded event loop to handle many tasks at once without creating new threads. This makes it efficient and scalable, especially for I/O-heavy operations.

12. **How does Node.js handle file I/O? Provide an example of reading a file
asynchronously?**
    - Node.js uses the `fs` module for file operations. Example:

    ```javascript
    const fs = require('fs');
    fs.readFile('example.txt', 'utf8', (err, data) => {
      if (err) throw err;
      console.log(data);
    });
    ```

13. **What are streams in Node.js and how are they useful?**
    - Streams let you handle data piece-by-piece instead of all at once, which is efficient for large files or data transfers. They use less memory and can start processing data immediately.

   ## Node.js Modules

1. **What are modules in Node.js and why are they important?**
   - Modules are reusable pieces of code that can be included in a Node.js application. They help organize code, promote reuse, and keep different functionalities separated, making the codebase more maintainable.

2. **How do you create a module in Node.js? Provide a simple example.**
   - To create a module, you define functions or variables in a file and export them. Example:
     ```javascript
     // math.js
     function add(a, b) {
       return a + b;
     }
     module.exports = add;
     ```

3. **Explain the difference between `require` and `import` statements in Node.js.**
   - `require`: Used in CommonJS, the default module system in Node.js. Synchronously loads modules.
   - `import`: Used in ES6 modules. Supports static imports and is asynchronous. Requires enabling with `"type": "module"` in `package.json` or using `.mjs` file extension.

4. **What is the `module.exports` object and how is it used?**
   - `module.exports` is an object that specifies what a module exports for use in other files. You assign values or functions to it to make them available outside the module.

5. **Describe how you can use the `exports` shorthand to export module contents.**
   - `exports` is a shorthand for `module.exports`. You can attach properties directly to `exports`, but you can't reassign it. Example:
     ```javascript
     // math.js
     exports.add = function(a, b) {
       return a + b;
     };
     ```

6. **What is the CommonJS module system?**
   - CommonJS is the default module system in Node.js. It uses `require` to import modules and `module.exports` to export them, allowing modularization of code.

7. **How can you import a module installed via NPM in your Node.js application?**
   - Use `require` to import the module by its package name. Example:
     ```javascript
     const express = require('express');
     ```

8. **Explain how the `path` module works in Node.js. Provide an example of using it.**
   - The `path` module provides utilities for working with file and directory paths. Example:
     ```javascript
     const path = require('path');
     const fullPath = path.join(__dirname, 'folder', 'file.txt');
     console.log(fullPath);
     ```

9. **How do you handle circular dependencies in Node.js modules?**
   - Circular dependencies occur when two or more modules depend on each other. Node.js handles them by returning a partially completed module during the cycle, which can lead to `undefined` values. Refactoring code to remove circular references is the best approach.

10. **What is a built-in module in Node.js? Name a few and explain their purposes.**
    - Built-in modules are modules that come with Node.js. Examples:
      - `fs`: File system operations (reading/writing files)
      - `http`: Building HTTP servers and clients
      - `path`: Working with file and directory paths
      - `os`: Provides information about the operating system

11. **What is the difference between relative and absolute module paths in Node.js?**
    - **Relative paths**: Start with `./` or `../` and are relative to the file location.
    - **Absolute paths**: Start from the root of the project directory.

12. **What is a module wrapper function in Node.js?**
    - Node.js wraps each module in a function before execution to provide scope isolation. This function has parameters like `exports`, `require`, `module`, `__filename`, and `__dirname`.

13. **Describe the `buffer` module and its use in Node.js.**
    - The `buffer` module provides a way to handle binary data directly in memory. It is used for tasks like reading from or writing to files, network communications, or interfacing with binary protocols. Example:
      ```javascript
      const buffer = Buffer.from('Hello, world!', 'utf8');
      console.log(buffer.toString('hex'));
      ```
## Starting an HTTP Server in Node.js

1. **How do you create a simple HTTP server in Node.js? Provide a code example.**
   - To create a simple HTTP server in Node.js, you use the http module, which provides the basic building blocks for building an HTTP server. The process involves importing the http module, creating the server, defining the request handler function, and starting the server to listen on a specific port.
   ```javascript
   const http = require('http');

   const server = http.createServer((req, res) => {
     res.statusCode = 200;
     res.setHeader('Content-Type', 'text/plain');
     res.end('Hello, world!\n');
   });

   const port = 3000;
   server.listen(port, () => {
     console.log(`Server running at http://localhost:${port}/`);
   });
   ```

2. **Explain the purpose of the `http` module in Node.js.**
   - The `http` module provides functionality for creating HTTP servers and making HTTP requests. It allows Node.js applications to handle client requests and serve responses over the web.

3. **What method do you use to start the HTTP server and make it listen on a specific port?**
   - Use the `listen` method of the HTTP server instance. Example:
     ```javascript
     server.listen(port, () => {
       console.log(`Server running at http://localhost:${port}/`);
     });
     ```

4. **How can you send a response to the client in an HTTP server created with Node.js?**
   - You can use the `res.writeHead` method to set the status code and headers, and the `res.end` method to send the response body. Example:
     ```javascript
     res.writeHead(200, { 'Content-Type': 'text/plain' });
     res.end('Hello, world!\n');
     ```

5. **Explain the request and response objects in the context of an HTTP server.**
   - **Request (`req`)**: Contains information about the client's request, including URL, HTTP method, headers, and any data sent in the request body.
   - **Response (`res`)**: Used to send back the desired HTTP response to the client, including status code, headers, and response body.

6. **How do you handle different HTTP methods (GET, POST, etc.) in a Node.js HTTP server?**
   - Check the `req.method` property to determine the HTTP method and handle accordingly. Example:
     ```javascript
     const server = http.createServer((req, res) => {
       if (req.method === 'GET') {
         res.end('GET request');
       } else if (req.method === 'POST') {
         res.end('POST request');
       }
     });
     ```

7. **What is middleware in the context of a Node.js HTTP server?**
   - Middleware refers to functions that process requests before they reach the final request handler. They can modify the request and response objects, handle errors, and perform tasks like authentication and logging.

8. **How can you serve static files using an HTTP server in Node.js?**
   - Use the `fs` module to read the file and serve its contents. Example:
     ```javascript
     const fs = require('fs');
     const path = require('path');

     const server = http.createServer((req, res) => {
       const filePath = path.join(__dirname, 'public', req.url === '/' ? 'index.html' : req.url);
       fs.readFile(filePath, (err, data) => {
         if (err) {
           res.statusCode = 404;
           res.end('File not found');
         } else {
           res.statusCode = 200;
           res.end(data);
         }
       });
     });
     ```

9. **Explain how to handle errors in an HTTP server created with Node.js.**
   - You can handle errors by checking for error conditions and sending appropriate responses. Example:
     ```javascript
     server.on('error', (err) => {
       console.error('Server error:', err);
     });

     const server = http.createServer((req, res) => {
       try {
         // Handle request
       } catch (err) {
         res.statusCode = 500;
         res.end('Internal server error');
       }
     });
     ```

10. **How can you implement routing in a Node.js HTTP server without using external libraries?**
    - Implement routing by checking the `req.url` and `req.method` properties. Example:
      ```javascript
      const server = http.createServer((req, res) => {
        if (req.url === '/' && req.method === 'GET') {
          res.end('Home page');
        } else if (req.url === '/about' && req.method === 'GET') {
          res.end('About page');
        } else {
          res.statusCode = 404;
          res.end('Page not found');
        }
      });
      ```
