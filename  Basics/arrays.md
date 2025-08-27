# JavaScript Arrays - Complete Guide 📚

## What is an Array?

An array is a special type of object that stores multiple values in a single variable. Think of it as a container that holds a list of items, like a shopping list or a collection of your favorite movies.

```javascript
// Simple array example
let fruits = ["apple", "banana", "orange"];
let numbers = [1, 2, 3, 4, 5];
let mixed = ["hello", 42, true, null];
```

---

## 🎯 Creating Arrays

### Method 1: Array Literal (Most Common)
```javascript
let colors = ["red", "green", "blue"];
let empty = [];
```

### Method 2: Array Constructor
```javascript
let fruits = new Array("apple", "banana", "orange");
let numbers = new Array(5); // Creates array with 5 empty slots
```

### Method 3: Array.from()
```javascript
let letters = Array.from("hello"); // ["h", "e", "l", "l", "o"]
let range = Array.from({length: 5}, (v, i) => i + 1); // [1, 2, 3, 4, 5]
```

---

## 🔍 Accessing Array Elements

### Index-Based Access
```javascript
let fruits = ["apple", "banana", "orange", "grape"];

// Accessing elements (index starts from 0)
console.log(fruits[0]);  // "apple" (first element)
console.log(fruits[1]);  // "banana" (second element)
console.log(fruits[-1]); // undefined (negative indices don't work)

// Last element access
console.log(fruits[fruits.length - 1]); // "grape"
```

### Using at() Method (Modern Approach)
```javascript
let fruits = ["apple", "banana", "orange", "grape"];

console.log(fruits.at(0));   // "apple"
console.log(fruits.at(-1));  // "grape" (last element)
console.log(fruits.at(-2));  // "orange" (second from end)
```

---

## 📊 Array Properties

### Length Property
```javascript
let animals = ["cat", "dog", "bird"];

console.log(animals.length); // 3

// Modify length
animals.length = 2; // Removes last element
console.log(animals); // ["cat", "dog"]

animals.length = 5; // Adds empty slots
console.log(animals); // ["cat", "dog", , , ]
```

---

## ➕ Adding Elements

### push() - Add to End
```javascript
let fruits = ["apple", "banana"];
fruits.push("orange");
console.log(fruits); // ["apple", "banana", "orange"]

// Add multiple elements
fruits.push("grape", "kiwi");
console.log(fruits); // ["apple", "banana", "orange", "grape", "kiwi"]
```

### unshift() - Add to Beginning
```javascript
let numbers = [2, 3, 4];
numbers.unshift(1);
console.log(numbers); // [1, 2, 3, 4]

// Add multiple elements
numbers.unshift(-1, 0);
console.log(numbers); // [-1, 0, 1, 2, 3, 4]
```

### splice() - Add at Specific Position
```javascript
let colors = ["red", "blue"];
colors.splice(1, 0, "green", "yellow"); // Insert at index 1
console.log(colors); // ["red", "green", "yellow", "blue"]
```

---

## ➖ Removing Elements

### pop() - Remove from End
```javascript
let fruits = ["apple", "banana", "orange"];
let removed = fruits.pop();
console.log(removed); // "orange"
console.log(fruits);  // ["apple", "banana"]
```

### shift() - Remove from Beginning
```javascript
let numbers = [1, 2, 3, 4];
let removed = numbers.shift();
console.log(removed); // 1
console.log(numbers); // [2, 3, 4]
```

### splice() - Remove from Specific Position
```javascript
let animals = ["cat", "dog", "bird", "fish"];
let removed = animals.splice(1, 2); // Remove 2 elements starting from index 1
console.log(removed); // ["dog", "bird"]
console.log(animals); // ["cat", "fish"]
```

### delete Operator
```javascript
let fruits = ["apple", "banana", "orange"];
delete fruits[1];
console.log(fruits); // ["apple", , "orange"] - creates empty slot
```

---

## 🔄 Modifying Arrays

### Changing Elements
```javascript
let fruits = ["apple", "banana", "orange"];
fruits[1] = "grape";
console.log(fruits); // ["apple", "grape", "orange"]
```

### fill() - Fill with Same Value
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.fill(0);
console.log(numbers); // [0, 0, 0, 0, 0]

// Fill specific range
let arr = [1, 2, 3, 4, 5];
arr.fill(9, 1, 3); // Fill from index 1 to 3 (exclusive)
console.log(arr); // [1, 9, 9, 4, 5]
```

### reverse() - Reverse Array
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.reverse();
console.log(numbers); // [5, 4, 3, 2, 1]
```

### sort() - Sort Array
```javascript
// String sorting
let fruits = ["banana", "apple", "orange"];
fruits.sort();
console.log(fruits); // ["apple", "banana", "orange"]

// Number sorting (need compare function)
let numbers = [10, 5, 40, 25, 1000, 1];
numbers.sort((a, b) => a - b); // Ascending
console.log(numbers); // [1, 5, 10, 25, 40, 1000]

numbers.sort((a, b) => b - a); // Descending
console.log(numbers); // [1000, 40, 25, 10, 5, 1]
```

---

## 🔍 Searching Methods

### indexOf() - Find Index
```javascript
let fruits = ["apple", "banana", "orange", "banana"];
console.log(fruits.indexOf("banana"));    // 1 (first occurrence)
console.log(fruits.indexOf("grape"));     // -1 (not found)
console.log(fruits.indexOf("banana", 2)); // 3 (search from index 2)
```

### lastIndexOf() - Find Last Index
```javascript
let numbers = [1, 2, 3, 2, 4];
console.log(numbers.lastIndexOf(2)); // 3 (last occurrence)
```

### includes() - Check if Element Exists
```javascript
let colors = ["red", "green", "blue"];
console.log(colors.includes("red"));    // true
console.log(colors.includes("yellow")); // false
```

### find() - Find First Matching Element
```javascript
let numbers = [5, 12, 8, 130, 44];
let found = numbers.find(num => num > 10);
console.log(found); // 12
```

### findIndex() - Find Index of First Match
```javascript
let numbers = [5, 12, 8, 130, 44];
let index = numbers.findIndex(num => num > 10);
console.log(index); // 1
```

---

## 🎯 Iteration Methods

### forEach() - Execute Function for Each Element
```javascript
let fruits = ["apple", "banana", "orange"];
fruits.forEach((fruit, index) => {
    console.log(`${index}: ${fruit}`);
});
// Output:
// 0: apple
// 1: banana  
// 2: orange
```

### map() - Transform Elements
```javascript
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

let fruits = ["apple", "banana"];
let upperFruits = fruits.map(fruit => fruit.toUpperCase());
console.log(upperFruits); // ["APPLE", "BANANA"]
```

### filter() - Filter Elements
```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6, 8, 10]

let words = ["apple", "banana", "kiwi", "orange"];
let longWords = words.filter(word => word.length > 5);
console.log(longWords); // ["banana", "orange"]
```

### reduce() - Reduce to Single Value
```javascript
let numbers = [1, 2, 3, 4, 5];

// Sum all numbers
let sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 15

// Find maximum
let max = numbers.reduce((max, num) => num > max ? num : max);
console.log(max); // 5

// Count occurrences
let fruits = ["apple", "banana", "apple", "orange", "banana"];
let count = fruits.reduce((acc, fruit) => {
    acc[fruit] = (acc[fruit] || 0) + 1;
    return acc;
}, {});
console.log(count); // {apple: 2, banana: 2, orange: 1}
```

---

## ✅ Testing Methods

### some() - Test if At Least One Element Passes
```javascript
let numbers = [1, 2, 3, 4, 5];
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

let ages = [12, 16, 18, 20];
let hasAdult = ages.some(age => age >= 18);
console.log(hasAdult); // true
```

### every() - Test if All Elements Pass
```javascript
let numbers = [2, 4, 6, 8];
let allEven = numbers.every(num => num % 2 === 0);
console.log(allEven); // true

let ages = [20, 25, 30, 17];
let allAdults = ages.every(age => age >= 18);
console.log(allAdults); // false
```

---

## ✂️ Extracting Parts

### slice() - Extract Portion (Non-destructive)
```javascript
let fruits = ["apple", "banana", "orange", "grape", "kiwi"];

console.log(fruits.slice(1, 3));    // ["banana", "orange"]
console.log(fruits.slice(2));       // ["orange", "grape", "kiwi"]
console.log(fruits.slice(-2));      // ["grape", "kiwi"]
console.log(fruits.slice(-3, -1));  // ["orange", "grape"]

console.log(fruits); // Original unchanged: ["apple", "banana", "orange", "grape", "kiwi"]
```

### splice() - Extract and Modify (Destructive)
```javascript
let numbers = [1, 2, 3, 4, 5];
let extracted = numbers.splice(1, 3); // Remove 3 elements starting from index 1
console.log(extracted); // [2, 3, 4]
console.log(numbers);   // [1, 5]
```

---

## 🔗 Joining Arrays

### concat() - Merge Arrays
```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];

let merged = arr1.concat(arr2, arr3);
console.log(merged); // [1, 2, 3, 4, 5, 6]

// Can also concat individual elements
let result = arr1.concat(7, 8);
console.log(result); // [1, 2, 7, 8]
```

### Spread Operator (Modern Approach)
```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];

let merged = [...arr1, ...arr2, ...arr3];
console.log(merged); // [1, 2, 3, 4, 5, 6]
```

---

## 📝 Converting Arrays

### join() - Array to String
```javascript
let fruits = ["apple", "banana", "orange"];

console.log(fruits.join());        // "apple,banana,orange"
console.log(fruits.join(" - "));   // "apple - banana - orange"
console.log(fruits.join(""));      // "applebananaorange"
```

### toString() - Array to String
```javascript
let numbers = [1, 2, 3, 4, 5];
console.log(numbers.toString()); // "1,2,3,4,5"
```

### Array.from() - Convert to Array
```javascript
// From string
let letters = Array.from("hello");
console.log(letters); // ["h", "e", "l", "l", "o"]

// From NodeList
let divs = Array.from(document.querySelectorAll('div'));

// From Set
let uniqueNumbers = Array.from(new Set([1, 2, 2, 3, 3, 4]));
console.log(uniqueNumbers); // [1, 2, 3, 4]
```

---

## 🆕 Modern Array Methods

### flat() - Flatten Nested Arrays
```javascript
let nested = [1, 2, [3, 4, [5, 6]]];
console.log(nested.flat());    // [1, 2, 3, 4, [5, 6]] (one level)
console.log(nested.flat(2));   // [1, 2, 3, 4, 5, 6] (two levels)
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5, 6] (all levels)
```

### flatMap() - Map then Flatten
```javascript
let sentences = ["hello world", "how are you"];
let words = sentences.flatMap(sentence => sentence.split(" "));
console.log(words); // ["hello", "world", "how", "are", "you"]
```

---

## 🎪 Practical Examples

### Example 1: Shopping Cart
```javascript
let cart = [];

// Add items
cart.push({name: "Laptop", price: 1000});
cart.push({name: "Mouse", price: 25});
cart.push({name: "Keyboard", price: 75});

// Calculate total
let total = cart.reduce((sum, item) => sum + item.price, 0);
console.log(`Total: $${total}`); // Total: $1100

// Find expensive items
let expensiveItems = cart.filter(item => item.price > 50);
console.log(expensiveItems);
```

### Example 2: Student Grades
```javascript
let students = [
    {name: "Alice", grade: 85},
    {name: "Bob", grade: 92},
    {name: "Charlie", grade: 78},
    {name: "Diana", grade: 96}
];

// Get all names
let names = students.map(student => student.name);
console.log(names); // ["Alice", "Bob", "Charlie", "Diana"]

// Find top performers (grade > 90)
let topStudents = students.filter(student => student.grade > 90);
console.log(topStudents);

// Calculate average grade
let averageGrade = students.reduce((sum, student) => sum + student.grade, 0) / students.length;
console.log(`Average Grade: ${averageGrade}`); // Average Grade: 87.75
```

### Example 3: Data Processing
```javascript
let data = "apple,banana,orange,apple,grape,banana";

// Convert to array and process
let fruits = data.split(",")
    .map(fruit => fruit.trim())           // Remove whitespace
    .filter(fruit => fruit !== "apple")   // Remove apples
    .sort();                             // Sort alphabetically

console.log(fruits); // ["banana", "banana", "grape", "orange"]

// Get unique fruits
let uniqueFruits = [...new Set(fruits)];
console.log(uniqueFruits); // ["banana", "grape", "orange"]
```

---

## 🚨 Common Mistakes to Avoid

### 1. Confusing Array Methods
```javascript
// ❌ Wrong - these modify original array
let numbers = [1, 2, 3];
numbers.sort();     // Modifies original
numbers.reverse();  // Modifies original
numbers.splice();   // Modifies original

// ✅ Correct - these create new arrays
let numbers = [1, 2, 3];
let sorted = [...numbers].sort();    // Original unchanged
let sliced = numbers.slice(1, 2);    // Original unchanged
let mapped = numbers.map(x => x * 2); // Original unchanged
```

### 2. Array Length Confusion
```javascript
// ❌ Wrong assumption
let arr = [1, 2, 3];
arr[10] = 10;
console.log(arr.length); // 11, not 4!
console.log(arr); // [1, 2, 3, , , , , , , , 10]
```

### 3. Reference vs Value
```javascript
// ❌ Wrong - copying reference
let original = [1, 2, 3];
let copy = original;
copy.push(4);
console.log(original); // [1, 2, 3, 4] - original changed!

// ✅ Correct - creating new array
let original = [1, 2, 3];
let copy = [...original]; // or original.slice()
copy.push(4);
console.log(original); // [1, 2, 3] - original unchanged
```

---

## 📋 Quick Reference Cheat Sheet

| Method | Modifies Original | Returns | Use Case |
|--------|------------------|---------|----------|
| `push()` | ✅ | New length | Add to end |
| `pop()` | ✅ | Removed element | Remove from end |
| `unshift()` | ✅ | New length | Add to beginning |
| `shift()` | ✅ | Removed element | Remove from beginning |
| `splice()` | ✅ | Removed elements | Add/remove at position |
| `slice()` | ❌ | New array | Extract portion |
| `concat()` | ❌ | New array | Join arrays |
| `map()` | ❌ | New array | Transform elements |
| `filter()` | ❌ | New array | Select elements |
| `reduce()` | ❌ | Single value | Accumulate result |
| `forEach()` | ❌ | undefined | Execute function |
| `find()` | ❌ | Element or undefined | Find first match |
| `includes()` | ❌ | Boolean | Check existence |
| `sort()` | ✅ | Sorted array | Sort elements |
| `reverse()` | ✅ | Reversed array | Reverse order |

---

**🎉 Congratulations!** You now have a comprehensive understanding of JavaScript arrays. Practice these methods with real examples to become proficient. Remember, the key to mastering arrays is understanding which methods modify the original array and which create new ones.