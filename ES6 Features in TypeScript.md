## Introduction

TypeScript does not only add types to JavaScript — it also allows you to use many **modern ES6 (ECMAScript 2015)** features today, while still compiling down to **ES5**, which runs in all browsers.

This means:
- You can write modern JavaScript
- Your code stays backward-compatible
- You get type safety and better tooling

⚠️ TypeScript does **not support 100% of ES6+ features**. Always check the official compatibility chart to see which features are supported.

This module introduces the **most commonly used ES6 features** in TypeScript.  
It is **not a full ES6 course**.

---

## `let` and `const`

### `var` vs `let`

```ts
var oldVariable = "test";
let newVariable = "test";
```

**Key difference: scope**

| Keyword | Scope |
|-------|------------|
| var  | Function / global scope |
| let |	Block scope |


Example: Block Scope

```ts
let value = "outside";

function reset() {
  let value = null;
  console.log(value); // null
}

reset();
console.log(value); // "outside"
```

* ➡️ The **let** variable inside the function does not overwrite the outer variable.

**const (Constants)**
```ts
const MAX_LEVEL = 100;
console.log(MAX_LEVEL);
// ❌ Error
MAX_LEVEL = 99;
```
* *const* values cannot be reassigned

* Encourages immutability

* Improves code clarity and safety

✅ Use const whenever a value should not change.

## Arrow Functions
### Traditional Function
```ts
function addNumbers(a: number, b: number): number {
  return a + b;
}

console.log(addNumbers(10, 3)); // 13
```

### Arrow Function Equivalent
```ts
const multiplyNumbers = (a: number, b: number): number => a * b;

console.log(multiplyNumbers(10, 3)); // 30
```

**Key Benefits**
* Shorter syntax

* Implicit return for single expressions

* Lexical **this** binding (important in classes & callbacks)

### Arrow Function Variations
**No Parameters**

```ts
const greet = () => {
  console.log("Hello");
};

greet();
```

**One Parameter (Parentheses Optional)**

```ts
const greetFriend = friend => {
  console.log(friend);
};

greetFriend("Manu");
```

⚠️ If you want **type annotations**, you must use parentheses:

```ts
const greetFriend = (friend: string) => {
  console.log(friend);
};
```

## Default Parameters

```ts
const countdown = (start: number = 10): void => {
  while (start > 0) {
    start--;
  }
  console.log("Done:", start);
};

countdown();     // Done: 0
countdown(20);   // Done: 0
```

***Rules***

* Default parameters must come **after** required parameters
 
* Defaults can depend on earlier parameters
  
```ts
const example = (a: number, b: number = a - 5) => {};
```

**❌ This is invalid:**

```ts
const example = (a: number = b - 5, b: number) => {};
```

## Spread Operator (...)
### Arrays → Value List

```ts
const numbers = [1, 10, 99, -5];

console.log(Math.max(...numbers)); // 99
```

**Combining Arrays**

```ts
const newArray = [66, 2];
newArray.push(...numbers);

console.log(newArray);
```

## Rest Operator (...)
### Value List → Array

**Rest Operator must be in last in parameter list**. Otherwise compiler error will thrown.

```ts
const makeArray = (...args: number[]): number[] => {
  return args;
};

console.log(makeArray(1, 2, 6)); // [1, 2, 6]
```

***With Other Parameters***
```ts
const logData = (name: string, ...values: number[]) => {
  console.log(name, values);
};

logData("Max", 1, 2, 3);
```

## Destructuring Arrays
### Traditional Way

```ts
const hobbies = ["Cooking", "Sports"];

const hobby1 = hobbies[0];
const hobby2 = hobbies[1];
```

**ES6 Destructuring**
```ts
const [hobby1, hobby2] = hobbies;

console.log(hobby1, hobby2);
```

## Destructuring Objects

```ts
const userData = {
  username: "Max",
  age: 27
};

const { username, age } = userData;
console.log(username, age);
```

### Aliases
```ts
const { username: myName, age: myAge } = userData;

console.log(myName, myAge);
```

## Template Literals
### String Concatenation (Old)

```ts
const name = "Max";
const greeting = "Hello, I'm " + name;
```

### Template Literal (ES6)

```ts
const greeting = `
Hello,
I'm ${name}
`;

console.log(greeting);
```

***Benefits***

* Multiline strings

* Easy variable interpolation

* Cleaner syntax

### Additional ES6 Features Supported by TypeScript
These are not covered deeply, but good to know:

* Classes

* Modules (import / export)

* Enhanced object literals

* Promises

* for...of loops

* Symbols

* Iterators & Generators

📌 Learn these in a dedicated ES6 course.

---
## Differences
### 1️⃣ concat vs join (Array methods)
**🔹 concat**

* Purpose: combine arrays (or values) → returns a new array

```ts
const a = [1, 2];
const b = [3, 4];

const result = a.concat(b);
console.log(result); // [1, 2, 3, 4]
```

- ✔ returns Array
- ✔ does not mutate original arrays
- ✔ works with arrays or single values

```ts
a.concat(5); // [1, 2, 5]
```

**🔹 join**

* Purpose: convert array → string

```ts
const a = [1, 2, 3];

const result = a.join("-");
console.log(result); // "1-2-3"
```

- ✔ returns string
- ✔ does not mutate array
- ✔ separator is optional (default is ",")
  
```ts
a.join();   // "1,2,3"
a.join(""); // "123"
```
---

## Exercises – Sample Solutions
### Exercise 1: Arrow Function
```ts
const double = (value: number): number => value * 2;
console.log(double(10));
```

### Exercise 2: Default Parameters
```ts
const greet = (name: string = "Max") => {
  console.log("Hello " + name);
};

greet();
greet("Anna");
```

### Exercise 3: Spread Operator with Math.min
```ts
const numbers = [5, 10, -3, 99];
console.log(Math.min(...numbers));
```

### Exercise 4: Pushing an Array
```ts
const newArray = [66, 2];
newArray.push(...numbers);

console.log(newArray);
```

### Exercise 5: Array Destructuring

```ts
const results = [1.5, 3.8, 7.2];
const [r1, r2, r3] = results;

console.log(r1, r2, r3);
```

### Exercise 6: Object Destructuring
```ts
const scientist = {
  firstName: "Will",
  experience: 12
};
const { firstName, experience } = scientist;
console.log(firstName, experience);
```

## Module Summary
You learned how TypeScript lets you safely use **modern ES6 syntax**:

* let and const

* Arrow functions

* Default parameters

* Spread & rest operators

* Destructuring

* Template literals

**These features help you write:**

* Cleaner code

* Safer code

* More expressive code

➡️ Combine ES6 + TypeScript to unlock the full power of modern JavaScript 🚀
