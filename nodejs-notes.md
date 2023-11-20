# Node.js Cheat Sheet

## Introduction to Node.js

What is Node.js? Node.js is an open-source, server-side runtime environment that allows you to run JavaScript code on the server.

Key Features:

- Non-blocking I/O operations.
- Event-driven, single-threaded architecture.
- Extensive package ecosystem with npm (Node Package Manager).

## Getting Started

Install Node.js: Download and install Node.js from nodejs.org.

Check Node.js Version: Verify your Node.js installation by running:

```
node -v
```

Create a Node.js Project: Create a directory for your project and run:

```
npm init
```

## Modules

CommonJS Modules: Node.js uses the CommonJS module system.

Import Modules: `Use require()` to import modules.

```
const fs = require('fs');
```

Export Modules: Create your own modules using module.exports.

```
// mymodule.js
module.exports = {
  greet: () => 'Hello, World!'
};
```

Core Modules
Node.js provides core modules for various functionalities like file system (fs), HTTP (http), and more.

Import core modules as needed.

## NPM (Node Package Manager)

Install Packages: Use npm install package-name to install packages locally.

Install Global Packages: Use -g flag to install packages globally.

Package.json: Manage project dependencies in package.json.

## Asynchronous Programming

Use callbacks, Promises, or async/await for asynchronous operations.

Example with Promises:

```
const readFilePromise = (filePath) => {
  return new Promise((resolve, reject) => {
    fs.readFile(filePath, 'utf8', (err, data) => {
      if (err) {
        reject(err);
        return;
      }
      resolve(data);
    });
  });
};
```

## HTTP Server

Create an HTTP server using the http module.

```
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, Node.js!');
});

const port = 3000;
server.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

## File System Operations

Read a file:

```
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

Write to a file:

```
fs.writeFile('file.txt', 'Hello, Node.js!', (err) => {
  if (err) throw err;
  console.log('File written');
});
```

## Event Emitter

Node.js uses the Event Emitter pattern for handling events.

```
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Register an event listener
emitter.on('event', () => {
  console.log('Event occurred');
});

// Emit an event
emitter.emit('event');
```

## Debugging

Use the built-in Node.js debugger with the `--inspect` flag.

```
node --inspect your-script.js
```

Alternatively, use external debugging tools like VS Code Debugger.
