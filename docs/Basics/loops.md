# 🔄 JavaScript Loops Guide

## 🤔 What are Loops?

Loops allow you to execute a block of code repeatedly. Think of them as a way to automate repetitive tasks!

**Real-world example:** Instead of writing `console.log()` 100 times, use a loop!

```javascript
// ❌ Without loops
console.log("Hello 1");
console.log("Hello 2");
console.log("Hello 3");

// ✅ With loops
for (let i = 1; i <= 3; i++) {
    console.log(`Hello ${i}`);
}
```

---

## 🔢 Types of Loops

### 1️⃣ **for Loop** - The Classic Counter

Use when you know exactly how many times to repeat.

```javascript
for (let i = 0; i < 5; i++) {
    console.log(`Count: ${i}`);
}
// Output: Count: 0, Count: 1, Count: 2, Count: 3, Count: 4
```

**Array iteration:**
```javascript
const fruits = ["apple", "banana", "orange"];

for (let i = 0; i < fruits.length; i++) {
    console.log(`Fruit ${i}: ${fruits[i]}`);
}
```

---

### 2️⃣ **while Loop** - The Condition Checker

Use when you don't know exact iterations but have a condition.

```javascript
let count = 0;
while (count < 3) {
    console.log(`Count: ${count}`);
    count++; // Don't forget to increment!
}
```

**Practical example:**
```javascript
let number = 16;
while (number > 1) {
    number = number / 2;
    console.log(number);
}
// Output: 8, 4, 2, 1
```

---

### 3️⃣ **do...while Loop** - Execute At Least Once

Executes code first, then checks condition.

```javascript
let num = 5;
do {
    console.log(`Number: ${num}`);
    num--;
} while (num > 0);
```

**Key difference from while:**
```javascript
let x = 5;

// This runs at least once even though condition is false
do {
    console.log("This will print once");
} while (x < 3);

// This won't run at all
while (x < 3) {
    console.log("This won't print");
}
```

---

### 4️⃣ **for...in Loop** - Object Properties

Iterates over object properties (keys).

```javascript
const person = {
    name: "Alice",
    age: 25,
    city: "New York"
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}
// Output: name: Alice, age: 25, city: New York
```

---

### 5️⃣ **for...of Loop** - Array Values

Iterates over array values directly.

```javascript
const colors = ["red", "green", "blue"];

for (let color of colors) {
    console.log(color);
}
// Output: red, green, blue
```

**String iteration:**
```javascript
const word = "HELLO";
for (let letter of word) {
    console.log(letter);
}
// Output: H, E, L, L, O
```

---

## 🚦 Loop Control

### **break** - Exit Loop

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 5) {
        break; // Stops at 5
    }
    console.log(i);
}
// Output: 0, 1, 2, 3, 4
```

### **continue** - Skip Current Iteration

```javascript
for (let i = 0; i < 5; i++) {
    if (i === 2) {
        continue; // Skip 2
    }
    console.log(i);
}
// Output: 0, 1, 3, 4
```

---

## ✅ Best Practices

### Choose the Right Loop:
```javascript
const numbers = [1, 2, 3, 4, 5];

// ✅ Use for...of for values
for (const num of numbers) {
    console.log(num * 2);
}

// ✅ Use traditional for when you need index
for (let i = 0; i < numbers.length; i++) {
    console.log(`Index ${i}: ${numbers[i]}`);
}

// ✅ Use for...in for object properties
const obj = { a: 1, b: 2 };
for (const key in obj) {
    console.log(`${key}: ${obj[key]}`);
}
```

### Common Patterns:
```javascript
// Reverse iteration
for (let i = array.length - 1; i >= 0; i--) {
    console.log(array[i]);
}

// Step by 2
for (let i = 0; i < 10; i += 2) {
    console.log(i); // 0, 2, 4, 6, 8
}
```

---

## 🚨 Common Mistakes

### 1. Infinite Loops
```javascript
// ❌ Wrong - infinite loop
let i = 0;
while (i < 5) {
    console.log(i);
    // Missing i++
}

// ✅ Correct
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

### 2. Array Index Errors
```javascript
const arr = [1, 2, 3];

// ❌ Wrong - goes out of bounds
for (let i = 0; i <= arr.length; i++) {
    console.log(arr[i]); // arr[3] is undefined
}

// ✅ Correct
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

### 3. Using for...in with Arrays
```javascript
const arr = [10, 20, 30];

// ❌ Avoid for arrays
for (let index in arr) {
    console.log(typeof index); // "string" not "number"
}

// ✅ Use for...of or traditional for
for (let value of arr) {
    console.log(value);
}
```

---

## 🎯 Quick Reference

| Loop | When to Use | Example |
|------|-------------|---------|
| `for` | Known iterations | `for(let i=0; i<5; i++)` |
| `while` | Condition-based | `while(condition)` |
| `do...while` | At least once | `do {...} while(condition)` |
| `for...in` | Object keys | `for(let key in obj)` |
| `for...of` | Array values | `for(let val of arr)` |

---

**💡 Remember:** Loops are fundamental for algorithms and data structure operations. Master them for efficient problem-solving!