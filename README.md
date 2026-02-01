# TypeScript

This repository is created to learn **TypeScript from scratch**, based on practical examples and core concepts.  
It explains *why TypeScript exists*, *how it improves JavaScript*, and *how to set up and use it in real projects*.

---

## What is TypeScript?

JavaScript is the scripting language used in browsers to make websites interactive.  
It supports features like constructor functions and prototypes, but it uses **dynamic typing**, meaning a variable’s type can change at runtime without any error.

**Example problem in JavaScript:**
A function expecting a string might accidentally receive an object, and JavaScript will not complain.

TypeScript solves this problem by introducing **static (strong) typing**.

### Key points:
- TypeScript is a **superset of JavaScript**
- Adds features like:
  - Static typing
  - Interfaces
  - Generics
- TypeScript **does not run in the browser**
- It must be compiled into JavaScript (usually ES5) using the TypeScript compiler

---

## Why TypeScript?

JavaScript allows code like this without errors:

```js
function Greeter(greeting) {
    this.greeting = greeting;
}

Greeter.prototype.greet = function() {
    return "Hello, " + this.greeting;
};

// Passing an object instead of a string
let greeter = new Greeter({ message: "world" });

let button = document.createElement('button');
button.textContent = "Say Hello";
button.onclick = function() {
    alert(greeter.greet());
};
```

**Problem**:
This outputs Hello, [object Object] instead of throwing an error.

# How TypeScript helps

In TypeScript, you can enforce types:
```js
class Greeter {
    greeting: string;

    constructor(greeting: string) {
        this.greeting = greeting;
    }

    greet() {
        return "Hello, " + this.greeting;
    }
}
```

Now, passing anything other than a string will cause a compile-time error, helping you catch bugs early.

# TypeScript Playground

You can experiment with TypeScript online using the official playground:

👉 https://www.typescriptlang.org/play

*It shows:*

TypeScript code

Compiled JavaScript output

Errors in real time

## Installing TypeScript
# Prerequisites

**Node.js** installed

**npm** (comes with Node.js)

Install TypeScript globally

**npm install -g typescript**


On Mac or Linux, you may need:

**sudo npm install -g typescript**

Using TypeScript

TypeScript files use the .ts extension

Browsers only understand JavaScript, so you must compile .ts → .js

Compile a TypeScript  named script.ts


**tsc script.ts**


This generates:

script.js

Important

In HTML files, always import the compiled .js file, not .ts.

Setting Up a TypeScript Project

#Initialize npm
**npm init**


Creates a ** package.json** file.

Install a lightweight development server

**npm install light-server --save-dev**


light-server:

Runs a local server

Automatically reloads the browser on changes

Initialize TypeScript configuration
**tsc --init**


Creates a **tsconfig.json** file.

Once this file exists, you can compile all TypeScript files by running:

***tsc***

# Important tsconfig.json Options

***Some key configuration options:***

**target** – JavaScript version to compile to (e.g. ES5)

**module** – Module system (CommonJS, ES6, etc.)

**outDir** – Folder for compiled JavaScript files

**rootDir** – Source folder for TypeScript files

**strict** – Enables strict type checking (recommended)

# Why Modules Need a Server

When using modules and multiple files:

Browsers block module loading via the ***file://*** protocol

A local server (like light-server) is required

This mimics real production environments

## Generics and Interfaces (Why They Matter)
# Interfaces

Define the structure of objects

Improve readability and consistency

Help catch missing or incorrect properties

# Generics

Allow reusable, type-safe components

Prevent duplication

Maintain flexibility without losing type safety

Together, they make TypeScript code:

Easier to maintain

More scalable

Less error-prone

# Project Structure (Suggested)
src/
 ├── basics/
 ├── interfaces/
 ├── generics/
 └── index.ts
dist/
tsconfig.json
package.json


