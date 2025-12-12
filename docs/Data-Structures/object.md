# JavaScript Objects - Complete Guide

## What is an Object?

Think of an object like a **real-world thing** that has characteristics and can do things.

**Example:** A car has:

- Properties (characteristics): color, brand, model, year
- Methods (actions): start(), stop(), accelerate()

In JavaScript, an object is a collection of **key-value pairs** where:

- **Key** = Property name (like "color")
- **Value** = Property value (like "red")

```javascript
let car = {
  color: "red",
  brand: "Toyota",
  year: 2020,
};
```

---

## Creating Objects

### 1. Object Literal (Most Common)

```javascript
let person = {
  name: "John",
  age: 25,
  city: "New York",
};
```

### 2. Using `new Object()`

```javascript
let person = new Object();
person.name = "John";
person.age = 25;
person.city = "New York";
```

### 3. Using Constructor Function

```javascript
function Person(name, age, city) {
  this.name = name;
  this.age = age;
  this.city = city;
}

let person1 = new Person("John", 25, "New York");
```

### 4. Using `Object.create()`

```javascript
let personPrototype = {
  greet: function () {
    console.log("Hello!");
  },
};

let person = Object.create(personPrototype);
person.name = "John";
```

### 5. Using ES6 Classes

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

let person = new Person("John", 25);
```

---

## Accessing Properties

### 1. Dot Notation

```javascript
let person = {
  name: "John",
  age: 25,
};

console.log(person.name); // "John"
console.log(person.age); // 25
```

### 2. Bracket Notation

```javascript
console.log(person["name"]); // "John"
console.log(person["age"]); // 25

// Useful when property name is dynamic
let property = "name";
console.log(person[property]); // "John"
```

---

## Modifying Objects

### Adding Properties

```javascript
let person = {
  name: "John",
};

person.age = 25; // dot notation
person["city"] = "NYC"; // bracket notation

console.log(person);
// { name: "John", age: 25, city: "NYC" }
```

### Updating Properties

```javascript
person.age = 26;
person["city"] = "Boston";
```

### Deleting Properties

```javascript
delete person.age;
console.log(person);
// { name: "John", city: "Boston" }
```

---

## Object Methods

Methods are **functions stored as object properties**.

```javascript
let calculator = {
  num1: 10,
  num2: 5,

  add: function () {
    return this.num1 + this.num2;
  },

  subtract: function () {
    return this.num1 - this.num2;
  },
};

console.log(calculator.add()); // 15
console.log(calculator.subtract()); // 5
```

### ES6 Method Shorthand

```javascript
let calculator = {
  num1: 10,
  num2: 5,

  add() {
    return this.num1 + this.num2;
  },

  subtract() {
    return this.num1 - this.num2;
  },
};
```

---

## Important Object Concepts

### 1. The `this` Keyword

`this` refers to the object that is executing the current function.

```javascript
let person = {
  name: "John",
  age: 25,

  introduce() {
    console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old`);
  },
};

person.introduce(); // "Hi, I'm John and I'm 25 years old"
```

### 2. Object Reference

Objects are stored by **reference**, not by value.

```javascript
let obj1 = { value: 10 };
let obj2 = obj1; // obj2 references the same object

obj2.value = 20;

console.log(obj1.value); // 20 (both changed!)
```

### 3. Copying Objects

#### Shallow Copy

```javascript
// Method 1: Object.assign()
let original = { a: 1, b: 2 };
let copy1 = Object.assign({}, original);

// Method 2: Spread operator
let copy2 = { ...original };
```

#### Deep Copy (for nested objects)

```javascript
let original = { a: 1, b: { c: 2 } };
let deepCopy = JSON.parse(JSON.stringify(original));
```

### 4. Checking Property Existence

```javascript
let person = { name: "John", age: 25 };

// Method 1: in operator
console.log("name" in person); // true
console.log("salary" in person); // false

// Method 2: hasOwnProperty()
console.log(person.hasOwnProperty("name")); // true

// Method 3: Direct check
console.log(person.name !== undefined); // true
```

---

## Common Object Operations

### 1. `Object.keys()` - Get all keys

```javascript
let person = { name: "John", age: 25, city: "NYC" };

let keys = Object.keys(person);
console.log(keys); // ["name", "age", "city"]
```

### 2. `Object.values()` - Get all values

```javascript
let values = Object.values(person);
console.log(values); // ["John", 25, "NYC"]
```

### 3. `Object.entries()` - Get key-value pairs

```javascript
let entries = Object.entries(person);
console.log(entries);
// [["name", "John"], ["age", 25], ["city", "NYC"]]
```

### 4. Looping Through Objects

#### For...in Loop

```javascript
for (let key in person) {
  console.log(`${key}: ${person[key]}`);
}
// name: John
// age: 25
// city: NYC
```

#### Using Object.keys()

```javascript
Object.keys(person).forEach((key) => {
  console.log(`${key}: ${person[key]}`);
});
```

#### Using Object.entries()

```javascript
Object.entries(person).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

### 5. `Object.freeze()` - Make object immutable

```javascript
let person = { name: "John", age: 25 };
Object.freeze(person);

person.age = 30; // Won't work
delete person.name; // Won't work
console.log(person); // { name: "John", age: 25 }
```

### 6. `Object.seal()` - Prevent adding/removing properties

```javascript
let person = { name: "John", age: 25 };
Object.seal(person);

person.age = 30; // Works (can modify existing)
person.city = "NYC"; // Won't work (can't add)
delete person.name; // Won't work (can't delete)
```

### 7. Merging Objects

```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { b: 3, c: 4 };

// Method 1: Object.assign()
let merged1 = Object.assign({}, obj1, obj2);

// Method 2: Spread operator
let merged2 = { ...obj1, ...obj2 };

console.log(merged2); // { a: 1, b: 3, c: 4 }
```

---

## Practice Problems

### Problem 1: Create a Student Object

```javascript
// Create a student with name, age, grades array, and a method to calculate average

let student = {
  name: "Alice",
  age: 20,
  grades: [85, 90, 92, 88],

  calculateAverage() {
    let sum = this.grades.reduce((acc, grade) => acc + grade, 0);
    return sum / this.grades.length;
  },
};

console.log(student.calculateAverage()); // 88.75
```

### Problem 2: Count Object Properties

```javascript
function countProperties(obj) {
  return Object.keys(obj).length;
}

let car = { brand: "Toyota", model: "Camry", year: 2020 };
console.log(countProperties(car)); // 3
```

### Problem 3: Check if Two Objects are Equal

```javascript
function areObjectsEqual(obj1, obj2) {
  let keys1 = Object.keys(obj1);
  let keys2 = Object.keys(obj2);

  if (keys1.length !== keys2.length) return false;

  for (let key of keys1) {
    if (obj1[key] !== obj2[key]) return false;
  }

  return true;
}

let a = { x: 1, y: 2 };
let b = { x: 1, y: 2 };
console.log(areObjectsEqual(a, b)); // true
```

### Problem 4: Filter Object by Value

```javascript
function filterObjectByValue(obj, minValue) {
  let result = {};

  for (let key in obj) {
    if (obj[key] >= minValue) {
      result[key] = obj[key];
    }
  }

  return result;
}

let scores = { math: 85, science: 92, english: 78, history: 88 };
console.log(filterObjectByValue(scores, 85));
// { math: 85, science: 92, history: 88 }
```

### Problem 5: Invert Object (Swap Keys and Values)

```javascript
function invertObject(obj) {
  let inverted = {};

  for (let key in obj) {
    inverted[obj[key]] = key;
  }

  return inverted;
}

let original = { a: "1", b: "2", c: "3" };
console.log(invertObject(original));
// { "1": "a", "2": "b", "3": "c" }
```

---

## Key Takeaways

1. ✅ Objects store data as key-value pairs
2. ✅ Access properties using dot (`.`) or bracket (`[]`) notation
3. ✅ Objects are **mutable** and passed by **reference**
4. ✅ Use `this` keyword to refer to the current object
5. ✅ Common methods: `Object.keys()`, `Object.values()`, `Object.entries()`
6. ✅ Objects can contain methods (functions)
7. ✅ Use `Object.freeze()` to make objects immutable
8. ✅ Spread operator (`...`) is useful for copying/merging objects

---

## Additional Resources

- [MDN Web Docs - Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- Practice on: [LeetCode](https://leetcode.com/), [HackerRank](https://www.hackerrank.com/)

---

**Happy Coding! 🚀**
