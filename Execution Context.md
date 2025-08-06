# JavaScript Execution Context & Call Stack

## 📝 Description

This document covers the fundamental concepts of JavaScript's Execution Context and Call Stack - essential building blocks for understanding how JavaScript code executes behind the scenes. 

**What you'll learn:**
- The technical definition and structure of Execution Contexts
- How JavaScript manages function calls using the Call Stack
- The two phases of code execution: Memory Creation and Code Execution
- Step-by-step breakdowns of real code examples
- Practice exercises to solidify your understanding

**Prerequisites:** Basic JavaScript syntax and functions

**Difficulty Level:** Beginner to Intermediate

**Estimated Reading Time:** 10-15 minutes

---

## 🧠 Theory: Execution Context (EC)

An **Execution Context** is the environment where JavaScript code runs. Every time a function runs, a new execution context is created.

### Types of Execution Contexts

1. **Global Execution Context (GEC)** – created when your JS file starts running
2. **Functional Execution Context (FEC)** – created every time a function is invoked
3. **Eval Execution Context** – created when `eval()` is used (rarely relevant in modern dev)

### What Technically Is an Execution Context?

Think of Execution Context as a "box" of data structures created whenever JavaScript starts running code — either globally or in a function.

**Internally, an EC consists of:**

1. **Memory/Variable Environment (Creation Phase)**:
   - All variables, functions, and arguments are stored here
   - Functions are stored fully; variables are stored with undefined (if var)

2. **Code Execution Phase**: 
   - Executes line-by-line
   - Assigns actual values to variables, runs functions

3. **this Binding**:
   - In global context: this → window (or global in Node)
   - In function: depends on how the function is called

### Each EC has:
- **Variable Environment (VE)**: memory allocated to variables/functions
- **Scope Chain**: the context it has access to
- **this binding**: value of this keyword

## 🧪 Call Stack

JavaScript is single-threaded. It uses a call stack to manage function calls.

```javascript
function a() {
    console.log("a");
    b();
}

function b() {
    console.log("b");
    c();
}

function c() {
    console.log("c");
}

a();
```

### 🔍 What happens here?

1. GEC created → code starts
2. `a()` is called → a()'s FEC pushed to call stack
3. Inside a, `b()` is called → FEC for b pushed
4. Inside b, `c()` is called → FEC for c pushed
5. c finishes → its EC is popped
6. Then b, then a, then GEC

## 📌 Example Breakdown

```javascript
function greet(name) {
    var message = "Hello " + name;
    return message;
}

var user = "Vijay";
var output = greet(user);
console.log(output);
```

### 🧠 Step-by-step:

**1. Global EC is created:**
- **Memory Phase:**
  - greet → [function]
  - user → undefined
  - output → undefined
  - console → [object]

**2. Code Execution Phase:**
- user → "Vijay"
- output → calls greet("Vijay")

**3. New EC for greet() is created:**
- **Memory:**
  - name → "Vijay"
  - message → undefined
- **Execution:**
  - message → "Hello Vijay"
  - Returns "Hello Vijay" → assigned to output

**4. GEC logs "Hello Vijay"**

## ✅ Practice Examples

### Example 1:
```javascript
console.log("start");

function foo() {
    console.log("inside foo");
}

foo();
console.log("end");
```

**Output Order:** start → inside foo → end

### Example 2:
```javascript
function outer() {
    function inner() {
        console.log("inner");
    }
    console.log("outer");
    inner();
}

outer();
```

**Output Order:** outer → inner

## 🎯 Key Takeaways

- Execution Context is a "box" of data structures that manages code execution
- JavaScript uses a call stack to manage function calls in LIFO (Last In, First Out) order
- Each context has two phases: Memory (Creation) and Code Execution
- Understanding EC is crucial for grasping hoisting, scope, and closures

---

**Next Topic**: Hoisting + Temporal Dead Zone (TDZ)
