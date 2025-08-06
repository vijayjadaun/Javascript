# JavaScript Hoisting & Temporal Dead Zone (TDZ)

## 📝 Description

This document explores JavaScript's hoisting mechanism and the Temporal Dead Zone (TDZ) - crucial concepts for understanding variable and function behavior during code execution. Learn why var, let, and const behave differently and how to avoid common pitfalls.

**What you'll learn:**
- How hoisting works behind the scenes
- The difference between var, let, and const hoisting
- What is Temporal Dead Zone and why it exists
- Function declarations vs expressions hoisting behavior
- Common interview questions and tricky scenarios

**Prerequisites:** Understanding of Execution Context and Call Stack

**Difficulty Level:** Intermediate

**Estimated Reading Time:** 15-20 minutes

---

## 🧠 What is Hoisting?

Hoisting is JavaScript's default behavior of moving declarations (not initializations) to the top of their scope before execution.

### 🔍 Two Key Rules:

1. **Function declarations** are hoisted entirely (definition + body)
2. **Variable declarations** (var, let, const) are hoisted, but:
   - **var**: initialized with undefined
   - **let & const**: not initialized → TDZ (explained below)

## 🔁 Memory & Execution Phases Reminder

Whenever a JS file or function runs:

**Memory Creation Phase:**
- JS engine scans for variables & functions
- Variables are hoisted (put in memory)
- Functions are fully hoisted (definition + body)

**Execution Phase:**
- Code is run line by line
- Values are assigned
- Errors may be thrown if accessing before initialization

## 🧪 Example: var Hoisting

```javascript
console.log(a); // undefined
var a = 5;
console.log(a); // 5
```

### 💡 Why?

**During memory phase:**
- a is hoisted as var a = undefined

**Execution phase:**
- console.log(a) → undefined
- a = 5
- console.log(a) → 5

## 🧨 But with let or const...

```javascript
console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

### 💣 Why?

- let and const are hoisted, but **not initialized**
- This uninitialized period is called the **Temporal Dead Zone (TDZ)**
- **TDZ** = time between hoisting and actual initialization where the variable exists but cannot be accessed

## 🔍 Visualization of TDZ

```javascript
let x = 10;

function demo() {
    console.log(x); // ❌ ReferenceError
    let x = 20;
}

demo();
```

The x inside demo() shadows the outer x and is in TDZ until its declaration line.

## ✅ Summary Table

| Type | Hoisted? | Initialized? | Can Access Before Line? |
|------|----------|--------------|-------------------------|
| var | Yes | With undefined | ✅ Yes (value = undefined) |
| let | Yes | ❌ No | ❌ No (TDZ) |
| const | Yes | ❌ No | ❌ No (TDZ) |

## 🧠 Important Interview Scenarios

### Example 1: var vs let

```javascript
function test() {
    console.log(a); // undefined
    console.log(b); // ReferenceError
    var a = 1;
    let b = 2;
}

test();
```

**Explanation:**
- a is hoisted & initialized → ✅ undefined
- b is hoisted but not initialized → ❌ ReferenceError (TDZ)

## 🧪 Practice Exercises

### Exercise 1: typeof Behavior

```javascript
console.log(typeof x); // ?
var x = 10;

console.log(typeof y); // ?
let y = 20;
```

**Answer:**
- typeof x → "undefined"
- typeof y → ReferenceError

**Explanation:**
- var x: hoisted and initialized with undefined, so typeof x is "undefined"
- let y: hoisted but not initialized, so accessing it (even with typeof) throws ReferenceError
- **Takeaway:** typeof is not "safe" for variables in TDZ

### Exercise 2: Function Declarations vs Expressions

```javascript
foo(); // ?
function foo() {
    console.log("hello");
}

bar(); // ?
var bar = function () {
    console.log("world");
};
```

**Answer:**
- foo() → "hello"
- bar() → TypeError: bar is not a function

**Explanation:**
- Function declarations are fully hoisted → foo() works
- var bar is hoisted with value undefined
- At the time of bar(), bar is still undefined, so undefined() throws TypeError

### Exercise 3: TDZ & Shadowing

```javascript
let name = "Vijay";

function sayHello() {
    console.log(name); // ?
    let name = "Pingu";
}

sayHello();
```

**Answer:**
- ReferenceError: Cannot access 'name' before initialization

**Explanation:**
- Inner let name = "Pingu" shadows the outer name
- When the engine reaches console.log(name), it sees the inner name — which is in TDZ
- So it throws ReferenceError, even though a name exists globally

## 🎯 Key Takeaways

- **JavaScript is parsed before executing** — so hoisting makes code behave differently than it looks
- **Avoid relying on hoisting behavior** for clean, bug-free code
- **var** gives undefined when accessed before declaration
- **let/const** throw ReferenceError when accessed before declaration (TDZ)
- **Function declarations** are fully hoisted, **function expressions** are not
- **typeof** is not safe for variables in TDZ

## 🚨 Best Practices

1. **Always declare variables before using them**
2. **Use let/const instead of var** for better error catching
3. **Declare functions before calling them** (even though declarations are hoisted)
4. **Be aware of variable shadowing** in nested scopes

---

**Next Topic**: Scope & Closures
