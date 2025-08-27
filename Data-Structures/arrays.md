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
**Time Complexity: O(1)** - Constant time
```javascript
let fruits = ["apple", "banana"];
fruits.push("orange");
console.log(fruits); // ["apple", "banana", "orange"]

// Add multiple elements
fruits.push("grape", "kiwi");
console.log(fruits); // ["apple", "banana", "orange", "grape", "kiwi"]
```

### unshift() - Add to Beginning
**Time Complexity: O(n)** - Linear time (needs to shift all existing elements)
```javascript
let numbers = [2, 3, 4];
numbers.unshift(1);
console.log(numbers); // [1, 2, 3, 4]

// Add multiple elements
numbers.unshift(-1, 0);
console.log(numbers); // [-1, 0, 1, 2, 3, 4]
```

### splice() - Add at Specific Position
**Time Complexity: O(n)** - Linear time (worst case when inserting at beginning)
```javascript
let colors = ["red", "blue"];
colors.splice(1, 0, "green", "yellow"); // Insert at index 1
console.log(colors); // ["red", "green", "yellow", "blue"]
```

---

## ➖ Removing Elements

### pop() - Remove from End
**Time Complexity: O(1)** - Constant time
```javascript
let fruits = ["apple", "banana", "orange"];
let removed = fruits.pop();
console.log(removed); // "orange"
console.log(fruits);  // ["apple", "banana"]
```

### shift() - Remove from Beginning
**Time Complexity: O(n)** - Linear time (needs to shift all remaining elements)
```javascript
let numbers = [1, 2, 3, 4];
let removed = numbers.shift();
console.log(removed); // 1
console.log(numbers); // [2, 3, 4]
```

### splice() - Remove from Specific Position
**Time Complexity: O(n)** - Linear time (worst case when removing from beginning)
```javascript
let animals = ["cat", "dog", "bird", "fish"];
let removed = animals.splice(1, 2); // Remove 2 elements starting from index 1
console.log(removed); // ["dog", "bird"]
console.log(animals); // ["cat", "fish"]
```

### delete Operator
**Time Complexity: O(1)** - Constant time (but creates sparse array)
```javascript
let fruits = ["apple", "banana", "orange"];
delete fruits[1];
console.log(fruits); // ["apple", , "orange"] - creates empty slot
```

---

## 🔄 Modifying Arrays

### Changing Elements
**Time Complexity: O(1)** - Constant time for direct access
```javascript
let fruits = ["apple", "banana", "orange"];
fruits[1] = "grape";
console.log(fruits); // ["apple", "grape", "orange"]
```

### fill() - Fill with Same Value
**Time Complexity: O(n)** - Linear time
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
**Time Complexity: O(n)** - Linear time
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.reverse();
console.log(numbers); // [5, 4, 3, 2, 1]
```

### sort() - Sort Array
**Time Complexity: O(n log n)** - Logarithmic time (typically using quicksort or mergesort)
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
**Time Complexity: O(n)** - Linear time (worst case)
```javascript
let fruits = ["apple", "banana", "orange", "banana"];
console.log(fruits.indexOf("banana"));    // 1 (first occurrence)
console.log(fruits.indexOf("grape"));     // -1 (not found)
console.log(fruits.indexOf("banana", 2)); // 3 (search from index 2)
```

### lastIndexOf() - Find Last Index
**Time Complexity: O(n)** - Linear time
```javascript
let numbers = [1, 2, 3, 2, 4];
console.log(numbers.lastIndexOf(2)); // 3 (last occurrence)
```

### includes() - Check if Element Exists
**Time Complexity: O(n)** - Linear time (worst case)
```javascript
let colors = ["red", "green", "blue"];
console.log(colors.includes("red"));    // true
console.log(colors.includes("yellow")); // false
```

### find() - Find First Matching Element
**Time Complexity: O(n)** - Linear time (worst case)
```javascript
let numbers = [5, 12, 8, 130, 44];
let found = numbers.find(num => num > 10);
console.log(found); // 12
```

### findIndex() - Find Index of First Match
**Time Complexity: O(n)** - Linear time (worst case)
```javascript
let numbers = [5, 12, 8, 130, 44];
let index = numbers.findIndex(num => num > 10);
console.log(index); // 1
```

---

## 🎯 Iteration Methods

### forEach() - Execute Function for Each Element
**Time Complexity: O(n)** - Linear time
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
**Time Complexity: O(n)** - Linear time
```javascript
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

let fruits = ["apple", "banana"];
let upperFruits = fruits.map(fruit => fruit.toUpperCase());
console.log(upperFruits); // ["APPLE", "BANANA"]
```

### filter() - Filter Elements
**Time Complexity: O(n)** - Linear time
```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6, 8, 10]

let words = ["apple", "banana", "kiwi", "orange"];
let longWords = words.filter(word => word.length > 5);
console.log(longWords); // ["banana", "orange"]
```

### reduce() - Reduce to Single Value
**Time Complexity: O(n)** - Linear time
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
**Time Complexity: O(n)** - Linear time (best case O(1) if first element matches)
```javascript
let numbers = [1, 2, 3, 4, 5];
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

let ages = [12, 16, 18, 20];
let hasAdult = ages.some(age => age >= 18);
console.log(hasAdult); // true
```

### every() - Test if All Elements Pass
**Time Complexity: O(n)** - Linear time (best case O(1) if first element fails)
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
**Time Complexity: O(n)** - Linear time relative to size of slice
```javascript
let fruits = ["apple", "banana", "orange", "grape", "kiwi"];

console.log(fruits.slice(1, 3));    // ["banana", "orange"]
console.log(fruits.slice(2));       // ["orange", "grape", "kiwi"]
console.log(fruits.slice(-2));      // ["grape", "kiwi"]
console.log(fruits.slice(-3, -1));  // ["orange", "grape"]

console.log(fruits); // Original unchanged: ["apple", "banana", "orange", "grape", "kiwi"]
```

### splice() - Extract and Modify (Destructive)
**Time Complexity: O(n)** - Linear time (worst case when removing from beginning)
```javascript
let numbers = [1, 2, 3, 4, 5];
let extracted = numbers.splice(1, 3); // Remove 3 elements starting from index 1
console.log(extracted); // [2, 3, 4]
console.log(numbers);   // [1, 5]
```

---

## 🔗 Joining Arrays

### concat() - Merge Arrays
**Time Complexity: O(n + m)** - Linear time relative to total length of all arrays
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
**Time Complexity: O(n + m)** - Linear time relative to total length of all arrays
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
**Time Complexity: O(n)** - Linear time
```javascript
let fruits = ["apple", "banana", "orange"];

console.log(fruits.join());        // "apple,banana,orange"
console.log(fruits.join(" - "));   // "apple - banana - orange"
console.log(fruits.join(""));      // "applebananaorange"
```

### toString() - Array to String
**Time Complexity: O(n)** - Linear time
```javascript
let numbers = [1, 2, 3, 4, 5];
console.log(numbers.toString()); // "1,2,3,4,5"
```

### Array.from() - Convert to Array
**Time Complexity: O(n)** - Linear time relative to source length
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
**Time Complexity: O(n)** - Linear time (where n is total elements at all levels)
```javascript
let nested = [1, 2, [3, 4, [5, 6]]];
console.log(nested.flat());    // [1, 2, 3, 4, [5, 6]] (one level)
console.log(nested.flat(2));   // [1, 2, 3, 4, 5, 6] (two levels)
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5, 6] (all levels)
```

### flatMap() - Map then Flatten
**Time Complexity: O(n)** - Linear time
```javascript
let sentences = ["hello world", "how are you"];
let words = sentences.flatMap(sentence => sentence.split(" "));
console.log(words); // ["hello", "world", "how", "are", "you"]
```

---

## ⚡ Time Complexity Summary

### Common Operations Time Complexities

| Operation | Method | Time Complexity | Space Complexity | Notes |
|-----------|--------|----------------|------------------|-------|
| **Access** | `arr[index]` | **O(1)** | O(1) | Direct index access |
| **Search** | `indexOf()`, `includes()` | **O(n)** | O(1) | Linear search |
| **Insert End** | `push()` | **O(1)** | O(1) | Amortized constant |
| **Insert Beginning** | `unshift()` | **O(n)** | O(1) | Shifts all elements |
| **Insert Middle** | `splice(index, 0, item)` | **O(n)** | O(1) | Shifts elements |
| **Delete End** | `pop()` | **O(1)** | O(1) | Constant time |
| **Delete Beginning** | `shift()` | **O(n)** | O(1) | Shifts all elements |
| **Delete Middle** | `splice(index, 1)` | **O(n)** | O(1) | Shifts elements |
| **Sort** | `sort()` | **O(n log n)** | O(log n) | Typically quicksort/mergesort |
| **Reverse** | `reverse()` | **O(n)** | O(1) | In-place reversal |
| **Copy** | `slice()`, `[...arr]` | **O(n)** | O(n) | Creates new array |
| **Iteration** | `forEach()`, `map()`, `filter()` | **O(n)** | O(1) to O(n) | Depends on callback |
| **Reduce** | `reduce()` | **O(n)** | O(1) | Single pass through array |
| **Join** | `concat()`, `[...arr1, ...arr2]` | **O(n + m)** | O(n + m) | Combined length |

### Performance Tips

#### ✅ Fast Operations (O(1))
```javascript
// These are very fast
arr[5] = "value";        // Direct assignment
arr.push(item);          // Add to end
let item = arr.pop();    // Remove from end
let length = arr.length; // Get length
```

#### ⚠️ Slower Operations (O(n))
```javascript
// These require shifting elements
arr.unshift(item);       // Add to beginning - shifts all elements
arr.shift();             // Remove from beginning - shifts all elements
arr.splice(0, 1);        // Remove from beginning - shifts all elements
arr.indexOf(item);       // Search through array
```

#### 🔄 When to Use What

```javascript
// ✅ For adding/removing at end - use push/pop
let stack = [];
stack.push(1);     // O(1)
stack.push(2);     // O(1)
stack.pop();       // O(1) - returns 2

// ❌ Avoid frequent operations at beginning
let arr = [1, 2, 3];
arr.unshift(0);    // O(n) - slow!
arr.shift();       // O(n) - slow!

// ✅ Better: Use proper data structures for queue operations
// Consider using a dedicated Queue implementation for frequent front operations
```

---

## 🎪 Practical Examples

### Example 1: Shopping Cart
```javascript
let cart = [];

// Add items - O(1) each
cart.push({name: "Laptop", price: 1000});
cart.push({name: "Mouse", price: 25});
cart.push({name: "Keyboard", price: 75});

// Calculate total - O(n)
let total = cart.reduce((sum, item) => sum + item.price, 0);
console.log(`Total: $${total}`); // Total: $1100

// Find expensive items - O(n)
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

// Get all names - O(n)
let names = students.map(student => student.name);
console.log(names); // ["Alice", "Bob", "Charlie", "Diana"]

// Find top performers (grade > 90) - O(n)
let topStudents = students.filter(student => student.grade > 90);
console.log(topStudents);

// Calculate average grade - O(n)
let averageGrade = students.reduce((sum, student) => sum + student.grade, 0) / students.length;
console.log(`Average Grade: ${averageGrade}`); // Average Grade: 87.75
```

### Example 3: Data Processing
```javascript
let data = "apple,banana,orange,apple,grape,banana";

// Convert to array and process - O(n) for each operation
let fruits = data.split(",")                    // O(n)
    .map(fruit => fruit.trim())                // O(n)
    .filter(fruit => fruit !== "apple")        // O(n)
    .sort();                                   // O(n log n)

console.log(fruits); // ["banana", "banana", "grape", "orange"]

// Get unique fruits - O(n)
let uniqueFruits = [...new Set(fruits)];
console.log(uniqueFruits); // ["banana", "grape", "orange"]
```

---

## 🚨 Common Mistakes to Avoid

### 1. Confusing Array Methods
```javascript
// ❌ Wrong - these modify original array
let numbers = [1, 2, 3];
numbers.sort();     // Modifies original - O(n log n)
numbers.reverse();  // Modifies original - O(n)
numbers.splice();   // Modifies original - O(n)

// ✅ Correct - these create new arrays
let numbers = [1, 2, 3];
let sorted = [...numbers].sort();    // Original unchanged - O(n log n)
let sliced = numbers.slice(1, 2);    // Original unchanged - O(n)
let mapped = numbers.map(x => x * 2); // Original unchanged - O(n)
```

### 2. Array Length Confusion
```javascript
// ❌ Wrong assumption
let arr = [1, 2, 3];
arr[10] = 10;        // O(1) but creates sparse array
console.log(arr.length); // 11, not 4!
console.log(arr); // [1, 2, 3, , , , , , , , 10]
```

### 3. Reference vs Value
```javascript
// ❌ Wrong - copying reference
let original = [1, 2, 3];
let copy = original;     // O(1) - just copying reference
copy.push(4);            // O(1) - but affects original!
console.log(original); // [1, 2, 3, 4] - original changed!

// ✅ Correct - creating new array
let original = [1, 2, 3];
let copy = [...original];  // O(n) - actual copy
copy.push(4);              // O(1) - affects only copy
console.log(original);     // [1, 2, 3] - original unchanged
```

---

## 📋 Quick Reference Cheat Sheet

| Method | Modifies Original | Returns | Time Complexity | Use Case |
|--------|------------------|---------|----------------|----------|
| `push()` | ✅ | New length | **O(1)** | Add to end |
| `pop()` | ✅ | Removed element | **O(1)** | Remove from end |
| `unshift()` | ✅ | New length | **O(n)** | Add to beginning |
| `shift()` | ✅ | Removed element | **O(n)** | Remove from beginning |
| `splice()` | ✅ | Removed elements | **O(n)** | Add/remove at position |
| `slice()` | ❌ | New array | **O(n)** | Extract portion |
| `concat()` | ❌ | New array | **O(n + m)** | Join arrays |
| `map()` | ❌ | New array | **O(n)** | Transform elements |
| `filter()` | ❌ | New array | **O(n)** | Select elements |
| `reduce()` | ❌ | Single value | **O(n)** | Accumulate result |
| `forEach()` | ❌ | undefined | **O(n)** | Execute function |
| `find()` | ❌ | Element or undefined | **O(n)** | Find first match |
| `includes()` | ❌ | Boolean | **O(n)** | Check existence |
| `sort()` | ✅ | Sorted array | **O(n log n)** | Sort elements |
| `reverse()` | ✅ | Reversed array | **O(n)** | Reverse order |
| `indexOf()` | ❌ | Index or -1 | **O(n)** | Find element index |
| `join()` | ❌ | String | **O(n)** | Array to string |

---

**🎉 Congratulations!** You now have a comprehensive understanding of JavaScript arrays including their time complexities. Understanding these performance characteristics will help you write more efficient code. Remember:

- Use `push()` and `pop()` for stack operations (O(1))
- Avoid frequent `unshift()` and `shift()` operations (O(n))  
- Consider the time complexity when working with large datasets
- Choose the right method based on your performance needs

Practice these methods with real examples and always consider the performance implications of your array operations!
