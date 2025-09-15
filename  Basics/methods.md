# JavaScript Methods Reference Guide 🚀

*A complete guide to JavaScript methods with practical examples for beginners*

---

## 📚 Array Methods

Arrays are like containers that hold multiple values. These methods help you work with them easily!

### 🔧 Modification Methods
*These methods change the original array*

#### `push()` - Add to the End
Adds one or more elements to the end of an array.
```javascript
let fruits = ['apple', 'banana'];
fruits.push('orange');
console.log(fruits); // ['apple', 'banana', 'orange']

// Add multiple items
fruits.push('mango', 'grape');
console.log(fruits); // ['apple', 'banana', 'orange', 'mango', 'grape']
```

#### `pop()` - Remove from the End
Removes and returns the last element from an array.
```javascript
let numbers = [1, 2, 3, 4];
let lastNumber = numbers.pop();
console.log(lastNumber); // 4
console.log(numbers); // [1, 2, 3]
```

#### `shift()` - Remove from the Beginning
Removes and returns the first element from an array.
```javascript
let colors = ['red', 'blue', 'green'];
let firstColor = colors.shift();
console.log(firstColor); // 'red'
console.log(colors); // ['blue', 'green']
```

#### `unshift()` - Add to the Beginning
Adds one or more elements to the beginning of an array.
```javascript
let animals = ['cat', 'dog'];
animals.unshift('bird');
console.log(animals); // ['bird', 'cat', 'dog']
```

#### `splice()` - Add/Remove at Any Position
The Swiss Army knife of array methods! Can add, remove, or replace elements anywhere.
```javascript
let items = ['a', 'b', 'c', 'd'];

// Remove 2 elements starting at index 1
items.splice(1, 2);
console.log(items); // ['a', 'd']

// Add elements at index 1
items.splice(1, 0, 'x', 'y');
console.log(items); // ['a', 'x', 'y', 'd']

// Replace elements
items.splice(1, 2, 'hello');
console.log(items); // ['a', 'hello', 'd']
```

#### `sort()` - Sort Elements
Sorts the elements of an array in place.
```javascript
// Simple sorting
let numbers = [3, 1, 4, 1, 5];
numbers.sort();
console.log(numbers); // [1, 1, 3, 4, 5]

// Custom sorting (for numbers)
let nums = [10, 5, 20, 15];
nums.sort((a, b) => a - b); // ascending
console.log(nums); // [5, 10, 15, 20]
```

#### `reverse()` - Reverse Order
Reverses the order of elements in an array.
```javascript
let letters = ['a', 'b', 'c'];
letters.reverse();
console.log(letters); // ['c', 'b', 'a']
```

#### `fill()` - Fill with a Value
Fills all or part of an array with a static value.
```javascript
let arr = new Array(5);
arr.fill(0);
console.log(arr); // [0, 0, 0, 0, 0]

// Fill specific positions
let nums = [1, 2, 3, 4, 5];
nums.fill(99, 1, 3); // fill from index 1 to 3
console.log(nums); // [1, 99, 99, 4, 5]
```

### 🔄 Iteration Methods
*These methods loop through arrays and perform operations*

#### `forEach()` - Execute Function for Each Element
Runs a function for every array element.
```javascript
let names = ['Alice', 'Bob', 'Charlie'];
names.forEach((name, index) => {
    console.log(`${index}: Hello ${name}!`);
});
// Output:
// 0: Hello Alice!
// 1: Hello Bob!
// 2: Hello Charlie!
```

#### `map()` - Transform Each Element
Creates a new array with the results of calling a function on every element.
```javascript
let numbers = [1, 2, 3, 4];
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
console.log(numbers); // [1, 2, 3, 4] (original unchanged)

// Real-world example
let users = [{name: 'John', age: 30}, {name: 'Jane', age: 25}];
let names = users.map(user => user.name);
console.log(names); // ['John', 'Jane']
```

#### `filter()` - Filter Elements
Creates a new array with elements that pass a test.
```javascript
let numbers = [1, 2, 3, 4, 5, 6];
let evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6]

// Filter objects
let products = [
    {name: 'laptop', price: 1000},
    {name: 'phone', price: 500},
    {name: 'tablet', price: 300}
];
let affordableProducts = products.filter(product => product.price < 600);
console.log(affordableProducts); // [{name: 'phone', price: 500}, {name: 'tablet', price: 300}]
```

#### `reduce()` - Reduce to Single Value
Reduces the array to a single value by applying a function.
```javascript
// Sum all numbers
let numbers = [1, 2, 3, 4, 5];
let sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 15

// Find maximum
let max = numbers.reduce((max, current) => current > max ? current : max);
console.log(max); // 5

// Group by property
let people = [
    {name: 'Alice', age: 25},
    {name: 'Bob', age: 30},
    {name: 'Charlie', age: 25}
];
let groupedByAge = people.reduce((groups, person) => {
    let age = person.age;
    groups[age] = groups[age] || [];
    groups[age].push(person);
    return groups;
}, {});
console.log(groupedByAge);
// {25: [{name: 'Alice', age: 25}, {name: 'Charlie', age: 25}], 30: [{name: 'Bob', age: 30}]}
```

#### `every()` - Test All Elements
Tests whether ALL elements pass a condition.
```javascript
let numbers = [2, 4, 6, 8];
let allEven = numbers.every(num => num % 2 === 0);
console.log(allEven); // true

let mixed = [2, 3, 4];
let allEvenMixed = mixed.every(num => num % 2 === 0);
console.log(allEvenMixed); // false
```

#### `some()` - Test Some Elements
Tests whether AT LEAST ONE element passes a condition.
```javascript
let numbers = [1, 3, 5, 8];
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true (because of 8)

let allOdd = [1, 3, 5, 7];
let hasEvenInOdd = allOdd.some(num => num % 2 === 0);
console.log(hasEvenInOdd); // false
```

#### `find()` - Find First Matching Element
Returns the first element that satisfies a condition.
```javascript
let users = [
    {id: 1, name: 'Alice'},
    {id: 2, name: 'Bob'},
    {id: 3, name: 'Charlie'}
];

let user = users.find(u => u.name === 'Bob');
console.log(user); // {id: 2, name: 'Bob'}

let notFound = users.find(u => u.name === 'David');
console.log(notFound); // undefined
```

#### `findIndex()` - Find Index of First Match
Returns the index of the first element that satisfies a condition.
```javascript
let numbers = [10, 20, 30, 40];
let index = numbers.findIndex(num => num > 25);
console.log(index); // 2 (index of 30)

let notFoundIndex = numbers.findIndex(num => num > 50);
console.log(notFoundIndex); // -1
```

### 🛠️ Utility Methods
*These methods help you work with arrays without changing them*

#### `concat()` - Merge Arrays
Combines two or more arrays into a new array.
```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];
let combined = arr1.concat(arr2, arr3);
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Using spread operator (modern way)
let modernCombined = [...arr1, ...arr2, ...arr3];
console.log(modernCombined); // [1, 2, 3, 4, 5, 6]
```

#### `slice()` - Extract Portion
Returns a shallow copy of a portion of an array.
```javascript
let fruits = ['apple', 'banana', 'orange', 'mango', 'grape'];
let someFruits = fruits.slice(1, 3);
console.log(someFruits); // ['banana', 'orange']
console.log(fruits); // Original unchanged

// Negative indices
let lastTwo = fruits.slice(-2);
console.log(lastTwo); // ['mango', 'grape']
```

#### `includes()` - Check if Element Exists
Determines whether an array includes a certain element.
```javascript
let colors = ['red', 'blue', 'green'];
console.log(colors.includes('blue')); // true
console.log(colors.includes('yellow')); // false

// Case sensitive
let names = ['Alice', 'Bob'];
console.log(names.includes('alice')); // false
```

#### `indexOf()` - Find Element Index
Returns the first index of an element, or -1 if not found.
```javascript
let letters = ['a', 'b', 'c', 'b', 'd'];
console.log(letters.indexOf('b')); // 1 (first occurrence)
console.log(letters.indexOf('z')); // -1 (not found)

// Starting from specific index
console.log(letters.indexOf('b', 2)); // 3 (search from index 2)
```

#### `join()` - Convert to String
Joins all elements into a string.
```javascript
let words = ['Hello', 'World', '!'];
let sentence = words.join(' ');
console.log(sentence); // "Hello World !"

let csvData = ['apple', 'banana', 'cherry'];
let csv = csvData.join(',');
console.log(csv); // "apple,banana,cherry"

// No separator
let letters = ['a', 'b', 'c'];
console.log(letters.join('')); // "abc"
```

#### `toString()` - Convert to String (Simple)
Converts an array to a comma-separated string.
```javascript
let numbers = [1, 2, 3];
console.log(numbers.toString()); // "1,2,3"

let mixed = [1, 'hello', true];
console.log(mixed.toString()); // "1,hello,true"
```

---

## 📝 String Methods

Strings are text data. These methods help you manipulate and work with text!

### ✂️ Manipulation Methods

#### `substring()` - Extract Part of String
Extracts characters between two indices.
```javascript
let text = "Hello World";
console.log(text.substring(0, 5)); // "Hello"
console.log(text.substring(6)); // "World"
console.log(text.substring(6, 11)); // "World"

// If start > end, they are swapped
console.log(text.substring(5, 0)); // "Hello"
```

#### `slice()` - Extract with Negative Indices
Similar to substring but supports negative indices.
```javascript
let text = "Hello World";
console.log(text.slice(0, 5)); // "Hello"
console.log(text.slice(6)); // "World"
console.log(text.slice(-5)); // "World" (last 5 characters)
console.log(text.slice(-5, -1)); // "Worl"
```

#### `replace()` - Replace Text
Replaces text in a string.
```javascript
let text = "Hello World";
let newText = text.replace("World", "JavaScript");
console.log(newText); // "Hello JavaScript"
console.log(text); // "Hello World" (original unchanged)

// Replace all occurrences with regex
let repeatedText = "cat dog cat bird cat";
let allReplaced = repeatedText.replace(/cat/g, "mouse");
console.log(allReplaced); // "mouse dog mouse bird mouse"

// Using replaceAll (modern browsers)
let allReplacedModern = repeatedText.replaceAll("cat", "mouse");
console.log(allReplacedModern); // "mouse dog mouse bird mouse"
```

#### `trim()` - Remove Whitespace
Removes whitespace from both ends of a string.
```javascript
let messy = "  Hello World  ";
console.log(messy.trim()); // "Hello World"
console.log(messy); // "  Hello World  " (original unchanged)

// Also trimStart() and trimEnd()
console.log(messy.trimStart()); // "Hello World  "
console.log(messy.trimEnd()); // "  Hello World"
```

#### `toUpperCase()` - Convert to Uppercase
Converts all characters to uppercase.
```javascript
let text = "Hello World";
console.log(text.toUpperCase()); // "HELLO WORLD"

// Useful for case-insensitive comparisons
let userInput = "YeS";
if (userInput.toUpperCase() === "YES") {
    console.log("User said yes!");
}
```

#### `toLowerCase()` - Convert to Lowercase
Converts all characters to lowercase.
```javascript
let text = "HELLO WORLD";
console.log(text.toLowerCase()); // "hello world"

// Email comparison example
let email1 = "User@Email.COM";
let email2 = "user@email.com";
console.log(email1.toLowerCase() === email2.toLowerCase()); // true
```

### 🔍 Search/Comparison Methods

#### `includes()` - Check if String Contains
Tests whether a string contains another string.
```javascript
let text = "Hello World";
console.log(text.includes("World")); // true
console.log(text.includes("world")); // false (case sensitive)
console.log(text.includes("Hello")); // true

// Check from specific position
console.log(text.includes("o", 5)); // true (finds 'o' in "World")
```

#### `indexOf()` - Find Position of Text
Returns the index of the first occurrence of specified text.
```javascript
let text = "Hello World Hello";
console.log(text.indexOf("Hello")); // 0
console.log(text.indexOf("World")); // 6
console.log(text.indexOf("hello")); // -1 (case sensitive)

// Find from specific position
console.log(text.indexOf("Hello", 1)); // 12 (second "Hello")
```

#### `startsWith()` - Check if String Starts With
Tests whether a string starts with specified characters.
```javascript
let url = "https://www.example.com";
console.log(url.startsWith("https")); // true
console.log(url.startsWith("http")); // true
console.log(url.startsWith("ftp")); // false

// Check from specific position
console.log(url.startsWith("www", 8)); // true
```

#### `endsWith()` - Check if String Ends With
Tests whether a string ends with specified characters.
```javascript
let filename = "document.pdf";
console.log(filename.endsWith(".pdf")); // true
console.log(filename.endsWith(".doc")); // false

let email = "user@gmail.com";
console.log(email.endsWith("gmail.com")); // true
```

### 🔧 Utility Methods

#### `split()` - Convert String to Array
Splits a string into an array based on a separator.
```javascript
let csv = "apple,banana,orange";
let fruits = csv.split(",");
console.log(fruits); // ["apple", "banana", "orange"]

let sentence = "Hello world from JavaScript";
let words = sentence.split(" ");
console.log(words); // ["Hello", "world", "from", "JavaScript"]

// Split each character
let text = "hello";
let characters = text.split("");
console.log(characters); // ["h", "e", "l", "l", "o"]

// Limit the number of splits
let limited = sentence.split(" ", 2);
console.log(limited); // ["Hello", "world"]
```

#### `charAt()` - Get Character at Index
Returns the character at a specified index.
```javascript
let text = "Hello";
console.log(text.charAt(0)); // "H"
console.log(text.charAt(4)); // "o"
console.log(text.charAt(10)); // "" (empty string for out of range)

// Alternative using bracket notation
console.log(text[0]); // "H"
console.log(text[4]); // "o"
```

#### `charCodeAt()` - Get Character Code
Returns the Unicode value of the character at a specified index.
```javascript
let text = "Hello";
console.log(text.charCodeAt(0)); // 72 (Unicode for 'H')
console.log(text.charCodeAt(1)); // 101 (Unicode for 'e')

// Useful for character comparisons
let char1 = "A";
let char2 = "B";
console.log(char1.charCodeAt(0) < char2.charCodeAt(0)); // true
```

---

## 🏗️ Object Methods

Objects are collections of key-value pairs. These methods help you work with object properties!

### 🔑 Property Handling Methods

#### `hasOwnProperty()` - Check if Property Exists
Tests whether an object has a specific property.
```javascript
let person = {name: "Alice", age: 30};

console.log(person.hasOwnProperty("name")); // true
console.log(person.hasOwnProperty("height")); // false

// Safer way to check (modern approach)
console.log(Object.hasOwnProperty.call(person, "name")); // true
```

#### `Object.keys()` - Get Property Names
Returns an array of an object's property names.
```javascript
let car = {
    brand: "Toyota",
    model: "Camry",
    year: 2022,
    color: "blue"
};

let keys = Object.keys(car);
console.log(keys); // ["brand", "model", "year", "color"]

// Loop through keys
keys.forEach(key => {
    console.log(`${key}: ${car[key]}`);
});
```

#### `Object.values()` - Get Property Values
Returns an array of an object's property values.
```javascript
let scores = {
    math: 95,
    english: 87,
    science: 92
};

let values = Object.values(scores);
console.log(values); // [95, 87, 92]

// Calculate average
let average = values.reduce((sum, score) => sum + score, 0) / values.length;
console.log(average); // 91.33
```

#### `Object.entries()` - Get Key-Value Pairs
Returns an array of key-value pairs.
```javascript
let product = {
    name: "Laptop",
    price: 999,
    inStock: true
};

let entries = Object.entries(product);
console.log(entries); 
// [["name", "Laptop"], ["price", 999], ["inStock", true]]

// Loop through entries
entries.forEach(([key, value]) => {
    console.log(`${key}: ${value}`);
});

// Convert back to object
let newObj = Object.fromEntries(entries);
console.log(newObj); // Same as original product object
```

#### `Object.assign()` - Copy/Merge Objects
Copies properties from source objects to a target object.
```javascript
let defaults = {color: "white", size: "medium"};
let userPrefs = {color: "blue", material: "cotton"};

let final = Object.assign({}, defaults, userPrefs);
console.log(final); // {color: "blue", size: "medium", material: "cotton"}

// Modern way using spread operator
let modernFinal = {...defaults, ...userPrefs};
console.log(modernFinal); // Same result

// Clone an object
let original = {a: 1, b: 2};
let clone = Object.assign({}, original);
console.log(clone); // {a: 1, b: 2}
```

#### `Object.freeze()` - Make Object Immutable
Prevents modifications to an object.
```javascript
let config = {
    apiUrl: "https://api.example.com",
    timeout: 5000
};

Object.freeze(config);

// These will silently fail (or throw error in strict mode)
config.apiUrl = "https://hacker.com";
config.newProp = "value";
delete config.timeout;

console.log(config); // Original object unchanged
console.log(Object.isFrozen(config)); // true
```

#### `Object.seal()` - Prevent Adding/Removing Properties
Allows modification of existing properties but prevents adding/removing.
```javascript
let user = {
    name: "Bob",
    email: "bob@email.com"
};

Object.seal(user);

// This works (modifying existing property)
user.name = "Robert";

// These don't work (adding/removing properties)
user.age = 30; // Won't be added
delete user.email; // Won't be deleted

console.log(user); // {name: "Robert", email: "bob@email.com"}
console.log(Object.isSealed(user)); // true
```

---

## 🔢 Number and Math Methods

Working with numbers and mathematical operations!

### 🔄 Number Conversion Methods

#### `parseInt()` - Convert to Integer
Parses a string and returns an integer.
```javascript
console.log(parseInt("123")); // 123
console.log(parseInt("123.45")); // 123 (decimal part ignored)
console.log(parseInt("123abc")); // 123 (stops at first non-digit)
console.log(parseInt("abc123")); // NaN

// Specify base (radix)
console.log(parseInt("1010", 2)); // 10 (binary to decimal)
console.log(parseInt("FF", 16)); // 255 (hexadecimal to decimal)

// Always specify radix for safety
let userInput = "08";
console.log(parseInt(userInput, 10)); // 8 (decimal)
```

#### `parseFloat()` - Convert to Float
Parses a string and returns a floating point number.
```javascript
console.log(parseFloat("123.45")); // 123.45
console.log(parseFloat("123.45abc")); // 123.45
console.log(parseFloat("abc123.45")); // NaN

// Scientific notation
console.log(parseFloat("1.23e2")); // 123
console.log(parseFloat("1.23e-2")); // 0.0123

// Use case: parsing user input
let priceString = "$19.99";
let price = parseFloat(priceString.replace("$", ""));
console.log(price); // 19.99
```

### 🧮 Math Operations

#### `Math.abs()` - Absolute Value
Returns the absolute (positive) value of a number.
```javascript
console.log(Math.abs(-5)); // 5
console.log(Math.abs(5)); // 5
console.log(Math.abs(-3.14)); // 3.14

// Use case: distance calculation
let point1 = 10;
let point2 = 3;
let distance = Math.abs(point1 - point2);
console.log(distance); // 7
```

#### `Math.round()` - Round to Nearest Integer
Rounds to the nearest integer.
```javascript
console.log(Math.round(4.3)); // 4
console.log(Math.round(4.7)); // 5
console.log(Math.round(4.5)); // 5
console.log(Math.round(-4.5)); // -4

// Round to specific decimal places
function roundTo(num, places) {
    let factor = Math.pow(10, places);
    return Math.round(num * factor) / factor;
}
console.log(roundTo(3.14159, 2)); // 3.14
```

#### `Math.floor()` - Round Down
Always rounds down to the nearest integer.
```javascript
console.log(Math.floor(4.9)); // 4
console.log(Math.floor(4.1)); // 4
console.log(Math.floor(-4.1)); // -5

// Use case: pagination
let totalItems = 47;
let itemsPerPage = 10;
let totalPages = Math.floor(totalItems / itemsPerPage) + 1;
console.log(totalPages); // 5
```

#### `Math.ceil()` - Round Up
Always rounds up to the nearest integer.
```javascript
console.log(Math.ceil(4.1)); // 5
console.log(Math.ceil(4.9)); // 5
console.log(Math.ceil(-4.9)); // -4

// Use case: calculating required batches
let items = 23;
let batchSize = 5;
let requiredBatches = Math.ceil(items / batchSize);
console.log(requiredBatches); // 5 batches needed
```

#### `Math.random()` - Random Number
Returns a random number between 0 (inclusive) and 1 (exclusive).
```javascript
console.log(Math.random()); // e.g., 0.7234567890123456

// Random integer between min and max (inclusive)
function randomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomInt(1, 6)); // Dice roll (1-6)
console.log(randomInt(10, 20)); // Random number 10-20

// Random array element
let colors = ['red', 'blue', 'green', 'yellow'];
let randomColor = colors[Math.floor(Math.random() * colors.length)];
console.log(randomColor);

// Random boolean
let randomBoolean = Math.random() < 0.5;
console.log(randomBoolean);
```

#### `Math.pow()` - Power/Exponent
Returns the value of x to the power of y.
```javascript
console.log(Math.pow(2, 3)); // 8 (2³)
console.log(Math.pow(5, 2)); // 25 (5²)
console.log(Math.pow(2, 0.5)); // 1.414... (square root of 2)

// Modern way using ** operator
console.log(2 ** 3); // 8
console.log(5 ** 2); // 25

// Use case: compound interest
let principal = 1000;
let rate = 0.05; // 5%
let years = 3;
let amount = principal * Math.pow(1 + rate, years);
console.log(amount); // 1157.625
```

#### `Math.sqrt()` - Square Root
Returns the square root of a number.
```javascript
console.log(Math.sqrt(16)); // 4
console.log(Math.sqrt(2)); // 1.414...
console.log(Math.sqrt(0)); // 0
console.log(Math.sqrt(-1)); // NaN

// Use case: distance between two points
function distance(x1, y1, x2, y2) {
    return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
}
console.log(distance(0, 0, 3, 4)); // 5
```

---

## ⚙️ Function Methods

These methods control how and where functions are executed!

#### `call()` - Call Function with Specific Context
Calls a function with a given `this` value and arguments.
```javascript
let person1 = {name: "Alice"};
let person2 = {name: "Bob"};

function greet(greeting, punctuation) {
    console.log(`${greeting}, I'm ${this.name}${punctuation}`);
}

// Call with different contexts
greet.call(person1, "Hello", "!"); // "Hello, I'm Alice!"
greet.call(person2, "Hi", "."); // "Hi, I'm Bob."

// Real-world example: borrowing methods
let numbers = [1, 2, 3, 4, 5];
let max = Math.max.call(null, ...numbers);
console.log(max); // 5
```

#### `apply()` - Call Function with Array Arguments
Similar to `call()` but takes arguments as an array.
```javascript
let person = {name: "Charlie"};

function introduce(greeting, age, city) {
    console.log(`${greeting}, I'm ${this.name}, ${age} years old from ${city}`);
}

let args = ["Hello", 30, "New York"];
introduce.apply(person, args);
// "Hello, I'm Charlie, 30 years old from New York"

// Use case: finding max in array (old way)
let numbers = [1, 5, 3, 9, 2];
let max = Math.max.apply(null, numbers);
console.log(max); // 9
```

#### `bind()` - Create Function with Fixed Context
Creates a new function with a permanently bound `this` value.
```javascript
let user = {
    name: "David",
    greet: function() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

// Problem: losing context
let greetFunc = user.greet;
greetFunc(); // "Hello, I'm undefined"

// Solution: bind the context
let boundGreet = user.greet.bind(user);
boundGreet(); // "Hello, I'm David"

// Partial application
function multiply(a, b) {
    return a * b;
}

let double = multiply.bind(null, 2);
console.log(double(5)); // 10 (2 * 5)

// Event handler example
let button = {
    name: "Submit Button",
    handleClick: function() {
        console.log(`${this.name} was clicked`);
    }
};

// Without bind, 'this' would refer to the button element
// document.getElementById('myButton').addEventListener('click', button.handleClick.bind(button));
```

---

## 📅 Date Methods

Working with dates and times!

#### `getDate()` - Get Day of Month
Returns the day of the month (1-31).
```javascript
let today = new Date();
console.log(today.getDate()); // e.g., 15

let specificDate = new Date('2024-03-25');
console.log(specificDate.getDate()); // 25
```

#### `getMonth()` - Get Month
Returns the month (0-11, where 0 = January).
```javascript
let today = new Date();
console.log(today.getMonth()); // ek