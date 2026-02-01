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

**In JavaScript:**
```js
let name = "Max"; // JS dynamically infers it's a string
name = 27; // ✅ Allowed in JS
```

**In TypeScript:**
```ts
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
let tripleAdd: [number, String, number, string] = [45, "Bhurulia", 25, "Gazipur Sadar"];// ✅ Allowed
```
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

---
### Functions as Types

You can define a function type:
```ts
let myMultiply: (val1: number, val2: number) => number;

myMultiply = multiply; // ✅ Correct
myMultiply = logMessage; // ❌ Error
```

Argument names do not matter; only types and return type are important.

---
### Objects and Types

TypeScript infers object structure:
```ts
let user = {
  name: "Max",
  age: 27
};

user.age = "27"; // ❌ Error
```

***Explicit object type:***
```ts
let userExplicit: { name: string; age: number } = {
  name: "Max",
  age: 27
};
```
---

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
### Type Aliases

Type aliases simplify reusing complex types:
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
---
### Union Types

Allow multiple types for a variable:
```ts
let course: string | number = "React";
course = 123; // ✅ Allowed
course = true; // ❌ Error
```
---
### Runtime Type Checking

Check types during runtime using typeof:
```ts
function printValue(value: number | string) {
  if (typeof value === "string") {
    console.log("String: " + value);
  } else {
    console.log("Number: " + value);
  }
}
```
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

With strictNullChecks: true:
```ts
let canBeNull: number | null = null; // ✅ Allowed
canBeNull = 12; // ✅ Allowed
canBeNull = undefined; // ❌ Error
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
