# TypeScript

This repository is created to learn **TypeScript from scratch**, based on practical examples and core concepts.  
It explains *why TypeScript exists*, *how it improves JavaScript*, and *how to set up and use it in real projects*.

---

## What is TypeScript?
A programming language to address short commings of js.

**Java Script** - Without Discipline

**Type Script** - with Discipline


Make on top of javascript with type chekcking.Every valid JavaScript file is also a valid TypeScript file, so you can gradually adopt it without rewriting your codebase. but ts  add some really cool features of js that help us build more robust and maintainable applications.

JavaScript is the scripting language used in browsers to make websites interactive.  
It supports features like constructor functions and prototypes, but it uses **dynamic typing**, meaning a variable’s type can change at runtime without any error.

***Staticaly Typed*** - C++, Java, C#, TS -> here Type determined in compile time

***Dynamically Typed*** - JavaScript, Python etc. -> Type determined in runtime


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

### How TypeScript helps

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

***TypeScript is more than just type checking.*** It enhances JavaScript in ways that **make development faster, safer, and more enjoyable.**

### 🚀 Smarter Development

Most modern code editors have excellent TypeScript support. This means they can:

**Detect the type** of your variables automatically

Provide **intelligent code completion**

**Offer refactoring tools** that make large-scale changes safer and easier

These features **boost productivity and reduce bugs** before your code even runs.

### ✨ Clearer and More Concise Code

TypeScript includes additional features that help you write cleaner, more maintainable code, making it easier to understand and collaborate on projects.

### 🌍 Using Future JavaScript Today

In JavaScript, different browsers may not implement all functions or features, which can lead to headaches.
With TypeScript, we can safely use modern JavaScript features, knowing that TypeScript will handle compatibility and prevent runtime issues.

### TypeScript Drawbacks
**1.** Needs always compilation otherwise browser can't detect it.
       ***.ts -> compiler -> .js***
this process is called traspilation

**2.** We need to added a bit more discipline when writing code.
**3.** Can't attach to a html file.


### TypeScript Playground

You can experiment with TypeScript online using the official playground:

👉 https://www.typescriptlang.org/play

**It shows:**

TypeScript code

Compiled JavaScript output

Errors in real time

## Installing TypeScript
### Prerequisites

**Node.js** installed

**npm** (comes with Node.js)

Install TypeScript globally

**npm install -g typescript**


On Mac or Linux, you may need:

**sudo npm install -g typescript**

Using TypeScript

TypeScript files use the **.ts** extension

Browsers only understand JavaScript, so you must compile **.ts → .js**

Compile a TypeScript  named **script.ts**


**tsc script.ts**


This generates:

script.js

Important

In HTML files, always import the compiled .js file, not .ts.

Setting Up a TypeScript Project

### Initialize npm
**npm init**


Creates a **package.json** file.

### Install and Configure a Lightweight Development Server

We use lite-server to run a local development server with live-reload support.

1. Install lite-server
```bash
npm install lite-server --save-dev 
```
2. Configure package.json

Update your ***package.json*** file as shown below:
```json
{
  "name": "typescriptprac",
  "version": "1.0.0",
  "description": "",
  "license": "ISC",
  "author": "",
  "type": "commonjs",
  "main": "index.js",
  "scripts": {
    "build": "tsc --project tsconfig.json",
    "start": "lite-server" // for ts compile and js run "concurrently \"tsc --watch\" \"lite-server\"" install concurrently first 'npm install --save-dev concurrently
'
  },
  "dependencies": {
    "reflect-metadata": "^0.2.2"
  },
  "devDependencies": {
    "lite-server": "^2.6.1"
  }
}
```
3. Run the Development Server

Start the local server:

***npm start***

4. Rebuild the Project

Compile the TypeScript files:

***npm run build***

About lite-server

Runs a local development server

Automatically reloads the browser when files change

### Initialize TypeScript configuration
**tsc --init**


Creates a **tsconfig.json** file.

Once this file exists, you can compile all TypeScript files by running:

***tsc***

### Important tsconfig.json Options

***Some key configuration options:***

**target** – JavaScript version to compile to (e.g. ES5)

**module** – Module system (CommonJS, ES6, etc.)

**outDir** – Folder for compiled JavaScript files

**rootDir** – Source folder for TypeScript files

**strict** – Enables strict type checking (recommended)

**removeComments** - Remove all comments in generated js file.

**noEmitOnError** - It will prevent for generating js file when ts file contains error.

**sourceMap** - Source map is a file that specifies how each line of our typeScript code maps to the generated code. when sourceMap = true, a file will generated after compilation.
              ***.js.map -***  This is not for us to understand. **This is for Debugger.**
              
---
### Create launch.json file
"preLaunchTask" : "tsp : build - tsconfig.json" // outside "compilerOptions" 
* All the spaces are matter here.

preLaunchTask is used to compile TypeScript before debugging starts.

TypeScript cannot run directly in Node or the browser. It must be compiled to JavaScript first.
This tells VS Code:

“Run the TypeScript build task before launching the debugger.”

***Why it’s needed***

* Ensures the latest .ts code is compiled

* Prevents debugging outdated or missing .js files

* Makes breakpoints and source maps work correctly


### Why Modules Need a Server

When using modules and multiple files:

Browsers block module loading via the ***file://*** protocol

A local server (like light-server) is required

This mimics real production environments

## Generics and Interfaces (Why They Matter)
### Interfaces

* Define the structure of objects

* Improve readability and consistency

* Help catch missing or incorrect properties

### Generics

* Allow reusable, type-safe components

* Prevent duplication

* Maintain flexibility without losing type safety

*Together, they make TypeScript code:*

* Easier to maintain

* More scalable

* Less error-prone

### Project Structure (Suggested)
```
src/
 ├── basics/
 ├── interfaces/
 ├── generics/
 └── index.ts
dist/
tsconfig.json
package.json
```

---
# TypeScript - Quick Q&A

1. **TypeScript Introduction – What is TypeScript?**  
A superset of JavaScript that adds static typing to catch errors early and improve code maintainability.

2. **Why TypeScript – Why do we need TS over JS?**  
To prevent runtime errors, improve code quality, and make large-scale projects easier to manage.

3. **JavaScript vs TypeScript – Key differences**  
JS is dynamically typed; TS is statically typed. TS must be compiled, JS runs directly in browsers.

4. **Superset Concept – What does TS as a superset mean?**  
Every valid JavaScript file is valid TypeScript. TS adds extra features on top of JS.

5. **Typing System – Static vs Dynamic typing**  
Static typing (TS) checks types at compile-time; dynamic typing (JS) checks at runtime.

6. **Type Safety – What problem does TS solve?**  
Catches type-related errors before code runs, reducing bugs.

7. **Compile Time vs Run Time – When are types checked?**  
TS checks types at compile-time; JS checks at run-time.

8. **Compilation – Why convert .ts to .js?**  
Browsers only understand JavaScript, so TS must be converted to JS to run.

9. **Transpilation – What is transpilation?**  
The process of converting TS code into JS code.

10. **Core Features – Main features of TypeScript**  
Static typing, interfaces, generics, modern JS support, better IDE tooling.

11. **Interfaces – Why use interfaces?**  
To define object structure, improve readability, and catch errors.

12. **Generics – Why use generics?**  
To create reusable, type-safe components without losing flexibility.

13. **tsconfig.json – Why is it important?**  
Configures how TypeScript compiles code, including target version, module type, and strictness.

14. **TypeScript Drawbacks – Limitations of TS**  
Requires compilation, extra setup, more disciplined coding, and cannot run directly in browsers.

15. **Project Structure – Why structure matters**  
Organized folders (src, dist, etc.) make code easier to maintain and scale.


