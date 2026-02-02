## Introduction

TypeScript is a superset of JavaScript that adds static types. This means you can define the type of variables, function arguments, return values, and more.

**Benefits of TypeScript:**

* Catch errors during development instead of runtime.

* IDE support with autocompletion and type hints.

* Safer and more maintainable code.

TypeScript code gets compiled into regular JavaScript. Types exist only during development; they do not appear in the compiled code.

---
## Type Basics

TypeScript's most important feature is types. 

| JavaScript | Extends in TypeScript |
|-----|------------|
| number | any |
| string | unknown |
| boolean | never |
| null   | enum |
| undefined | tuple |
| object |  |

* TypeScript compiler can detect variable based on their values like 123-456-789 detect as a number
* If we don't initialize variable, it's type will be 'any' 

**In JavaScript:**
```js
let name = "Max"; // JS dynamically infers it's a string
name = 27; // ✅ Allowed in JS
```

**In TypeScript:**
```ts
let age; // it will be any type. So, it can assign in any type.
age = 12;  ✅ Allowed 
age = "123";  ✅ Allowed 

let name = "Max"; // TypeScript infers type string
name = 27; // ❌ Error: Type 'number' is not assignable to type 'string'
```

TypeScript uses type inference automatically, but you can also assign types explicitly.

---
### Numbers and Booleans

Basic types include:
```ts
let age = 27; // number
let hasHobbies = true; // boolean

age = "27"; // ❌ Error
hasHobbies = 1; // ❌ Error
```

**Notes:**

* TypeScript does not differentiate between integers and floats. Both are number.

* Boolean values can only be true or false.
  
---
### Assigning Types Explicitly

Sometimes, you might want to declare a variable without initializing:
```ts
let myRealAge: number; // explicit type
myRealAge = 27; 
myRealAge = "27"; // ❌ Error
```

The ***any*** type allows flexibility but removes type safety:
```ts
let myRealAgeAny: any;
myRealAgeAny = 27;
myRealAgeAny = "27"; // ✅ Allowed
```
---
### Arrays and Types

Arrays can hold multiple values of the same type:
```ts
let emptyArray = []; // empty array will 'any' type like js. So, we need to annotated it when declare.
let hobbies: string[] = ["Sports", "Cooking"];
hobbies = [100]; // ❌ Error

let flexibleArray: any[] = ["Hello", 42, true]; // ✅ Allowed
```
---
### Tuples

Tuples are arrays with fixed types and order:
```ts
let address: [string, number] = ["Main St", 99];
address = [99, "Main St"]; // ❌ Error
let fullAddress: [number, String, number, string] = [45, "Bhurulia", 25, "Gazipur Sadar"];// ✅ Allowed
```
* After compilation it will be a regular js array.
* If we use ***fullAddress.*** we can use all functions and propertie of that type.
* If we use ***fullAddress.push(1);*** no error will generate. **It is a gap of TS.** 
---
### Enums

Enums allow human-readable names for numeric values:
```ts
enum Color {
  Red,    // 0
  Green,  // 1
  Blue    // 2
}

let myColor: Color = Color.Green; // 1

enum Status {
  Pending = 3,
  Approved, // 4
  Rejected  // 5
}
```
If we declare enum as const enum, compiler wil generate more optimize code in js file.
```ts
const enum Status {
  Pending = 3,
  Approved, // 4
  Rejected  // 5
}
console.log(Status.Approved);
```
***in JS***
```js
"use strict";
console.log(4 /* Status.Approved */);
```

---
### The any Type

any disables type checking:
```ts
let something: any = "Hello";
something = 42; // ✅ Allowed
```

⚠ Use sparingly to maintain safety.

---
## Understanding the Generated JavaScript

TypeScript compiles away all types. For example:

```ts
let name: string = "Max";
```

***Compiles to:***
```js
var name = "Max"; // types removed
```

Enums are converted into self-executing functions to map names to numbers.

---
### Types in Functions
```ts
//function render(doc) { // ❌ Error: will show an error. Because by default "noImplicitAny" : true; so we should explicity define it as 
function render(doc : any) { 
  console.log(doc);
}
```
***To Prevent this type of error we can set noImplicitAny = false. But it will loose the Features of Type safety.***

You can type arguments and return values:
```ts
function multiply(a: number, b: number): number {
  return a * b;
}

function logMessage(message: string): void {
  console.log(message);
}
```

* void = function returns nothing.

* Return type mismatch triggers compile errors.
  
* ***If function doesn't have any return type, then ts compiler inferred the return type.***
**
* If there are any unused parameters in function and we need a warning for this, enable **"noUnsedParameters"** in tsConfig.json file.

* If not all code path has return statement then compiler will not throw error. Because JS by default returns undefined.
  **to get this error in compiler time set "noImplicitReturns" : true in tsConfig.json**
```js
function calc (inc : number) {
  if(inc>50000) return inc*12;
}
```
* If a local variable is unsed, and wants to get a warning for that enable **"noUnusedLocals"**

* In TypeScript, if a function defines two parameters, you must pass exactly two arguments when calling it.
but in JavaScript, functions are more flexible and do not enforce the number of arguments.

* If a parameter is optional in TypeScript, you can mark it using ***?***.

***Optional Parameters (?)***

An optional parameter may be **undefined**, so you usually need to handle that case.
```ts
function greet(name: string, title?: string) {
  const finalTitle = title || "Guest";
  console.log(`Hello ${finalTitle} ${name}`);
}

greet("Alice");          // Hello Guest Alice
greet("Bob", "Mr.");     // Hello Mr. Bob
```

Here, ***|| is used as a fallback trick*** to handle optional values.

***Best Practice: Default Parameters ✅***

* Instead of using ||, the recommended approach is to assign a default value directly in the function parameters.
  
```ts
function greet(name: string, title: string = "Guest") {
  console.log(`Hello ${title} ${name}`);
}

greet("Alice");          // Hello Guest Alice
greet("Bob", "Mr.");     // Hello Mr. Bob
```

* Default parameters are clearer, safer, and avoid unexpected behavior with falsy values like "" or 0.

---
### Functions as Types

You can define a function type:
```ts
let func;
func = multiply; // ✅ Correct
func = logMessage; // ✅ Correct

let myMultiply: (val1: number, val2: number) => number;

myMultiply = multiply; // ✅ Correct
myMultiply = logMessage; // ❌ Error
```

Argument names do not matter; only types and return type are important.

---
### Objects and Types
* In JavaScript, objects are dynamic, which means you can add or remove properties at any time.
```js
const user = { name: "Alice" };
user.age = 25; // ✅ Allowed in JavaScript
```

* In TypeScript, object shapes are strictly enforced. You cannot add arbitrary properties that are not defined in the object’s type.
```ts
const user: { name: string } = { name: "Alice" };
user.age = 25; // ❌ Error: Property 'age' does not exist
```

* This helps catch bugs at compile time and makes the code more predictable.
* TypeScript infers object structure:
```ts
let user = {
  name: "Max",
  age: 27
};

user.age = "27"; // ❌ Error
user = {  // ❌ Error
  a: "Max",  // ❌ Error Because property names are impotant in TS
  b: 27  // ❌ Error
};  // ❌ Error

```
***Explicit object type:***
```ts
let userExplicit: { name: string; age: number } = {
  name: "Max",
  age: 27
};
```
**Optional Properties (?)**
In TypeScript, object properties can be marked as optional using ***?***.
Optional properties ***do not need to be initialized*** when the object is created.
```ts
type User = {
  name: string;
  age?: number;
};

const user1: User = { name: "Alice" };        // ✅ valid
const user2: User = { name: "Bob", age: 30 }; // ✅ valid
```

* Optional properties are useful when certain data may or may not be present.

***Extra Tip 🧠***

* Even though optional properties are allowed, you should still check for their existence before using them:
```ts
if (user2.age !== undefined) {
  console.log(user2.age);
}
```

### Complex Objects

Combine types in objects:
```ts
let complex: { data: number[]; output: (all: boolean) => number[] } = {
  data: [100, 3.99, 10],
  output: function(all: boolean): number[] {
    return this.data;
  }
};
```
---

## Advance Type
### Type Aliases
* When creating multiple objects with the same structure, rewriting the full object shape each time violates the DRY (Don’t Repeat Yourself) principle.
To avoid this, TypeScript provides Type Aliases, which let us define an object’s shape in one place and reuse it everywhere.

* Type aliases simplify reusing complex types:
```ts
type BankAccount = { money: number; deposit: (value: number) => void };
type Person = { name: string; bankAccount: BankAccount; hobbies: string[] };

let bankAccount: BankAccount = {
  money: 2000,
  deposit(value: number) {
    this.money += value;
  }
};

let myself: Person = {
  name: "Max",
  bankAccount: bankAccount,
  hobbies: ["Sports", "Cooking"]
};
```
*This makes the code easier to maintain and more consistent.

---
### Union Type (|)
* Union types allow a variable or parameter to accept more than one type.

```ts
let course: string | number = "React";
course = 123; // ✅ Allowed
course = true; // ❌ Error
//Runtime Type Checking
function kgToLbs(weight: number | string): number {
  if (typeof weight === "number") {
    // weight is treated as number here.
    return weight * 2.2;
  } else {
    // weight is treated as string here
    return parseInt(weight) * 2.2;
  }
}
```
**User-defined types Union:**

Example 1:
```ts
type Admin = {
  role: "admin";
  permissions: string[];
};

type Customer = {
  role: "customer";
  purchases: number;
};

type User = Admin | Customer;
//Runtime Type Checking
function printUser(user: User) {
  if (user.role === "admin") {
    console.log(user.permissions);
  } else {
    console.log(user.purchases);
  }
}
```
Example 2:
```ts
type A = {
  foo(): void;
};

type B = {
  bar(): void;
};

type C = A | B;

const obj1: C = {
  foo() {
    console.log("foo");
  }
}; // ✅ valid

const obj2: C = {
  bar() {
    console.log("bar");
  }
}; // ✅ valid

const obj3: C = {
  foo() {},
  bar() {}
}; // ✅ এটাও valid

```

### Intersection Types (&)

* Intersection types combine multiple types into one, requiring all properties from each type.
```ts
type Draggable = {
  drag: () => void;
};

type Resizable = {
  resize: () => void;
};

type UIWidget = Draggable & Resizable;

let textBar: UIWidget = {
  drag: () => {
    console.log("Dragging");
  },
  resize: () => {
    console.log("Resizing");
  }
};
```

***Here, textBar must implement both drag and resize.***

---

### Literal Types

* Literal types restrict values to specific exact values, improving type safety.
```ts
let quantity: 50 = 50;
// quantity = 100 ❌ not allowed

let quantity: 50 | 100 = 50;
// can also assign 100

type Quantity = 50 | 100 | 150 | 200;
let quan: Quantity = 100;
// cannot assign any value other than 50, 100, 150, 200

let metrics: "cm" | "m" | "km" = "cm";
```

Literal types are useful when only a fixed set of values is allowed.

---
### The never Type

never is used for functions that never return:
```ts
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}
```

Different from void (void functions finish execution but return nothing).

---
### Nullable Types

With **strictNullChecks: true** (by default true when "strict" :true) :
```ts
let canNull = null // means canNull: null . here null is behave like a type
canNull = 12; ❌ Error Can't assign value without null

let canBeNull: number | null = null; // ✅ Allowed
canBeNull = 12; // ✅ Allowed
canBeNull = undefined; // ❌ Error

let canNumNUllUnd : number | null | undefined;
canNumNUllUnd = 12; // ✅ Allowed
canNumNUllUnd = undefined; // ✅ Allowed
```

* Variables initialized with null are inferred as null.

* Use union types for safe null handling.

---
### Module Exercise

**Task:** Convert this JavaScript code to TypeScript:
```ts
const bankAccount = {
  money: 2000,
  deposit(value) {
    this.money += value;
  }
};

const myself = {
  name: "Max",
  bankAccount: bankAccount,
  hobbies: ["Sports", "Cooking"]
};
```

***Solution (TypeScript):***
```ts
type BankAccount = { money: number; deposit: (value: number) => void };
type Person = { name: string; bankAccount: BankAccount; hobbies: string[] };

const bankAccount: BankAccount = {
  money: 2000,
  deposit(value: number) {
    this.money += value;
  }
};

const myself: Person = {
  name: "Max",
  bankAccount: bankAccount,
  hobbies: ["Sports", "Cooking"]
};
```
---

### Summary & Best Practices

* Types make your programs safer and easier to maintain.

* Use type aliases for reusable structures.

* Use never for impossible code paths.

* Enable strictNullChecks to prevent null/undefined bugs.

* Prefer explicit types for complex structures, optional for simple variables.
