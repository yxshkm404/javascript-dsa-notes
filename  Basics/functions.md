# JavaScript Functions - Complete Guide 📚

## What is a Function?

A function is a reusable block of code that performs a specific task. Think of it as a recipe - you write it once and can use it multiple times with different ingredients (inputs) to get different results (outputs).

```javascript
// Simple function example
function greet(name) {
    return "Hello, " + name + "!";
}

console.log(greet("Alice")); // "Hello, Alice!"
console.log(greet("Bob"));   // "Hello, Bob!"
```

### Why Use Functions?
- **Reusability**: Write once, use many times
- **Organization**: Keep code clean and structured
- **Modularity**: Break complex problems into smaller parts
- **Maintainability**: Easier to update and debug

---

## 🎯 Creating Functions

### 1. Function Declaration (Hoisted)
```javascript
// Function is available before declaration due to hoisting
sayHello(); // This works!

function sayHello() {
    console.log("Hello World!");
}

// Function with parameters
function add(a, b) {
    return a + b;
}

console.log(add(5, 3)); // 8
```

### 2. Function Expression (Not Hoisted)
```javascript
// This would cause an error if called before declaration
// sayGoodbye(); // ❌ Error!

const sayGoodbye = function() {
    console.log("Goodbye!");
};

sayGoodbye(); // ✅ Works

// Named function expression
const multiply = function multiplyNumbers(x, y) {
    return x * y;
};

console.log(multiply(4, 5)); // 20
```

### 3. Arrow Functions (ES6)
```javascript
// Basic arrow function
const greet = () => {
    console.log("Hello from arrow function!");
};

// With parameters
const subtract = (a, b) => {
    return a - b;
};

// Shorthand for single expression
const square = x => x * x;
const isEven = num => num % 2 === 0;

// Multiple parameters need parentheses
const divide = (a, b) => a / b;

console.log(square(5));    // 25
console.log(isEven(4));    // true
console.log(divide(10, 2)); // 5
```

### 4. Function Constructor (Rarely Used)
```javascript
const sum = new Function('a', 'b', 'return a + b');
console.log(sum(2, 3)); // 5
```

---

## 📋 Function Anatomy

```javascript
function functionName(parameter1, parameter2) {
    // Function body
    let result = parameter1 + parameter2;
    return result; // Return statement
}

// Calling/Invoking the function
let answer = functionName(5, 10);
```

### Parts Explained:
- **`function`**: Keyword that declares a function
- **`functionName`**: Name of the function (should be descriptive)
- **`(parameter1, parameter2)`**: Parameters (inputs the function expects)
- **`{}`**: Function body (code that runs when function is called)
- **`return`**: Sends a value back to whoever called the function
- **`functionName(5, 10)`**: Function call with arguments

---

## 🔄 Parameters vs Arguments

```javascript
// Parameters are variables in function definition
function introduce(name, age) {  // name and age are parameters
    return `Hi, I'm ${name} and I'm ${age} years old.`;
}

// Arguments are actual values passed to function
let message = introduce("Sarah", 25);  // "Sarah" and 25 are arguments
console.log(message); // "Hi, I'm Sarah and I'm 25 years old."
```

### Default Parameters
```javascript
function greetUser(name = "Guest", greeting = "Hello") {
    return `${greeting}, ${name}!`;
}

console.log(greetUser());                    // "Hello, Guest!"
console.log(greetUser("Alice"));             // "Hello, Alice!"
console.log(greetUser("Bob", "Welcome"));    // "Welcome, Bob!"
```

### Rest Parameters (...args)
```javascript
function sumAll(...numbers) {
    let total = 0;
    for (let num of numbers) {
        total += num;
    }
    return total;
}

console.log(sumAll(1, 2, 3));        // 6
console.log(sumAll(1, 2, 3, 4, 5));  // 15
console.log(sumAll());               // 0

// Mixed parameters
function introduce(name, ...hobbies) {
    return `${name} likes: ${hobbies.join(", ")}`;
}

console.log(introduce("Alice", "reading", "painting", "hiking"));
// "Alice likes: reading, painting, hiking"
```

---

## 🔙 Return Statement

### Basic Return
```javascript
function calculateArea(length, width) {
    return length * width;
}

let area = calculateArea(5, 3);
console.log(area); // 15
```

### Multiple Return Points
```javascript
function checkAge(age) {
    if (age < 0) {
        return "Invalid age";
    }
    
    if (age < 18) {
        return "Minor";
    }
    
    if (age < 65) {
        return "Adult";
    }
    
    return "Senior";
}

console.log(checkAge(16)); // "Minor"
console.log(checkAge(30)); // "Adult"
console.log(checkAge(70)); // "Senior"
```

### Returning Objects and Arrays
```javascript
function createUser(name, email) {
    return {
        name: name,
        email: email,
        id: Math.random().toString(36)
    };
}

function getFirstAndLast(arr) {
    return [arr[0], arr[arr.length - 1]];
}

let user = createUser("John", "john@email.com");
let endpoints = getFirstAndLast([1, 2, 3, 4, 5]);

console.log(user);      // {name: "John", email: "john@email.com", id: "..."}
console.log(endpoints); // [1, 5]
```

### Functions Without Return
```javascript
function logMessage(message) {
    console.log(message);
    // No return statement - function returns undefined
}

let result = logMessage("Hello!");
console.log(result); // undefined
```

---

## 🏗️ Function Types & Patterns

### 1. Pure Functions
Functions that always return the same output for the same input and have no side effects.

```javascript
// ✅ Pure function
function add(a, b) {
    return a + b;
}

function multiply(x, y) {
    return x * y;
}

// ❌ Impure function (side effects)
let counter = 0;
function incrementCounter() {
    counter++; // Modifies external variable
    return counter;
}

// ❌ Impure function (different outputs)
function getRandomNumber() {
    return Math.random(); // Different output each time
}
```

### 2. Higher-Order Functions
Functions that take other functions as arguments or return functions.

```javascript
// Function that takes another function as argument
function processArray(arr, callback) {
    let result = [];
    for (let item of arr) {
        result.push(callback(item));
    }
    return result;
}

const double = x => x * 2;
const square = x => x * x;

let numbers = [1, 2, 3, 4, 5];
console.log(processArray(numbers, double)); // [2, 4, 6, 8, 10]
console.log(processArray(numbers, square)); // [1, 4, 9, 16, 25]

// Function that returns another function
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const triple = createMultiplier(3);
const quadruple = createMultiplier(4);

console.log(triple(5));     // 15
console.log(quadruple(5));  // 20
```

### 3. Anonymous Functions
Functions without names, often used as callbacks.

```javascript
// Anonymous function in setTimeout
setTimeout(function() {
    console.log("This runs after 1 second");
}, 1000);

// Anonymous arrow function
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(x => x * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Anonymous function in event handling (if in browser)
// button.addEventListener('click', function() {
//     console.log('Button clicked!');
// });
```

### 4. IIFE (Immediately Invoked Function Expression)
Functions that run as soon as they're defined.

```javascript
// Basic IIFE
(function() {
    console.log("This runs immediately!");
})();

// IIFE with parameters
(function(name) {
    console.log(`Hello, ${name}!`);
})("World");

// IIFE that returns a value
let result = (function(a, b) {
    return a + b;
})(5, 3);

console.log(result); // 8

// Arrow IIFE
(() => {
    console.log("Arrow IIFE!");
})();
```

---

## 🎯 Scope and Closures

### Function Scope
```javascript
let globalVar = "I'm global";

function outerFunction() {
    let outerVar = "I'm in outer function";
    
    function innerFunction() {
        let innerVar = "I'm in inner function";
        
        console.log(globalVar); // ✅ Accessible
        console.log(outerVar);  // ✅ Accessible
        console.log(innerVar);  // ✅ Accessible
    }
    
    innerFunction();
    // console.log(innerVar); // ❌ Error! Not accessible here
}

outerFunction();
// console.log(outerVar); // ❌ Error! Not accessible here
```

### Closures
A closure is when an inner function has access to variables from its outer function even after the outer function has finished executing.

```javascript
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

let counter1 = createCounter();
let counter2 = createCounter();

console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter1()); // 3

console.log(counter2()); // 1 (independent counter)
console.log(counter2()); // 2

// Practical closure example
function createBankAccount(initialBalance) {
    let balance = initialBalance;
    
    return {
        deposit: function(amount) {
            balance += amount;
            return balance;
        },
        withdraw: function(amount) {
            if (amount <= balance) {
                balance -= amount;
                return balance;
            }
            return "Insufficient funds";
        },
        getBalance: function() {
            return balance;
        }
    };
}

let account = createBankAccount(100);
console.log(account.deposit(50));   // 150
console.log(account.withdraw(30));  // 120
console.log(account.getBalance());  // 120
```

---

## 🔄 `this` Keyword in Functions

### Regular Functions
```javascript
const person = {
    name: "Alice",
    age: 30,
    greet: function() {
        console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
    },
    celebrateBirthday: function() {
        this.age++;
        console.log(`Happy birthday! Now I'm ${this.age} years old.`);
    }
};

person.greet(); // "Hi, I'm Alice and I'm 30 years old."
person.celebrateBirthday(); // "Happy birthday! Now I'm 31 years old."
```

### Arrow Functions and `this`
```javascript
const person = {
    name: "Bob",
    regularFunction: function() {
        console.log("Regular function this:", this.name); // "Bob"
        
        const arrowFunction = () => {
            console.log("Arrow function this:", this.name); // "Bob" (inherits from parent)
        };
        
        arrowFunction();
    }
};

person.regularFunction();

// Arrow functions don't have their own 'this'
const obj = {
    name: "Charlie",
    arrowMethod: () => {
        console.log(this.name); // undefined (or window.name in browser)
    }
};

obj.arrowMethod();
```

---

## 🎪 Built-in Function Methods

### call(), apply(), bind()
```javascript
const person1 = { name: "Alice" };
const person2 = { name: "Bob" };

function introduce(greeting, punctuation) {
    console.log(`${greeting}, I'm ${this.name}${punctuation}`);
}

// call() - arguments passed individually
introduce.call(person1, "Hello", "!");    // "Hello, I'm Alice!"
introduce.call(person2, "Hi", ".");       // "Hi, I'm Bob."

// apply() - arguments passed as array
introduce.apply(person1, ["Hey", "!!"]);  // "Hey, I'm Alice!!"
introduce.apply(person2, ["Greetings", "."]); // "Greetings, I'm Bob."

// bind() - creates new function with bound 'this'
const aliceIntroduce = introduce.bind(person1);
aliceIntroduce("Welcome", "!"); // "Welcome, I'm Alice!"

const bobSayHi = introduce.bind(person2, "Hi");
bobSayHi("!"); // "Hi, I'm Bob!"
```

---

## 🎯 Common Function Patterns

### 1. Callback Pattern
```javascript
function processData(data, callback) {
    // Simulate async operation
    setTimeout(() => {
        const result = data.toUpperCase();
        callback(result);
    }, 1000);
}

processData("hello world", function(result) {
    console.log("Processed:", result); // "Processed: HELLO WORLD"
});
```

### 2. Factory Pattern
```javascript
function createCalculator(type) {
    if (type === "basic") {
        return {
            add: (a, b) => a + b,
            subtract: (a, b) => a - b
        };
    } else if (type === "scientific") {
        return {
            add: (a, b) => a + b,
            subtract: (a, b) => a - b,
            multiply: (a, b) => a * b,
            divide: (a, b) => a / b,
            power: (a, b) => Math.pow(a, b)
        };
    }
}

const basicCalc = createCalculator("basic");
const scientificCalc = createCalculator("scientific");

console.log(basicCalc.add(5, 3));        // 8
console.log(scientificCalc.power(2, 3));  // 8
```

### 3. Module Pattern
```javascript
const MathUtils = (function() {
    // Private variables and functions
    let pi = 3.14159;
    
    function validateNumber(num) {
        return typeof num === 'number' && !isNaN(num);
    }
    
    // Public API
    return {
        circleArea: function(radius) {
            if (!validateNumber(radius)) {
                return "Invalid input";
            }
            return pi * radius * radius;
        },
        
        circleCircumference: function(radius) {
            if (!validateNumber(radius)) {
                return "Invalid input";
            }
            return 2 * pi * radius;
        },
        
        getPi: function() {
            return pi;
        }
    };
})();

console.log(MathUtils.circleArea(5));  // 78.53975
console.log(MathUtils.getPi());        // 3.14159
// console.log(MathUtils.pi);          // undefined (private)
```

---

## 🚀 Advanced Function Concepts

### 1. Recursion
Functions that call themselves.

```javascript
// Factorial example
function factorial(n) {
    // Base case
    if (n <= 1) {
        return 1;
    }
    
    // Recursive case
    return n * factorial(n - 1);
}

console.log(factorial(5)); // 120 (5 * 4 * 3 * 2 * 1)

// Countdown example
function countdown(num) {
    console.log(num);
    
    if (num > 1) {
        countdown(num - 1);
    } else {
        console.log("Blast off! 🚀");
    }
}

countdown(5);
// Output: 5, 4, 3, 2, 1, "Blast off! 🚀"

// Fibonacci sequence
function fibonacci(n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(6)); // 8 (0, 1, 1, 2, 3, 5, 8)
```

### 2. Memoization
Caching function results for better performance.

```javascript
function memoize(fn) {
    const cache = {};
    
    return function(...args) {
        const key = JSON.stringify(args);
        
        if (cache[key]) {
            console.log("Cache hit!");
            return cache[key];
        }
        
        console.log("Computing...");
        const result = fn(...args);
        cache[key] = result;
        return result;
    };
}

// Expensive function
function expensiveCalculation(n) {
    let result = 0;
    for (let i = 0; i < n * 1000000; i++) {
        result += i;
    }
    return result;
}

const memoizedCalc = memoize(expensiveCalculation);

console.log(memoizedCalc(5)); // "Computing..." then result
console.log(memoizedCalc(5)); // "Cache hit!" then result (much faster)
```

### 3. Currying
Breaking down functions with multiple arguments into a series of functions with single arguments.

```javascript
// Regular function
function add(a, b, c) {
    return a + b + c;
}

// Curried version
function curriedAdd(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}

// Arrow function version
const curriedAddArrow = a => b => c => a + b + c;

console.log(add(1, 2, 3));                    // 6
console.log(curriedAdd(1)(2)(3));             // 6
console.log(curriedAddArrow(1)(2)(3));        // 6

// Practical currying example
const createMultiplier = factor => number => number * factor;

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15

// Partial application
const addToTen = curriedAdd(10);
const addToTenAndFive = addToTen(5);

console.log(addToTenAndFive(3)); // 18 (10 + 5 + 3)
```

---

## 🎯 Array Methods with Functions

### map(), filter(), reduce()
```javascript
const numbers = [1, 2, 3, 4, 5];

// map() - transform each element
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

const squared = numbers.map(function(num) {
    return num * num;
});
console.log(squared); // [1, 4, 9, 16, 25]

// filter() - select elements that meet criteria
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4]

const greaterThanThree = numbers.filter(function(num) {
    return num > 3;
});
console.log(greaterThanThree); // [4, 5]

// reduce() - accumulate into single value
const sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 15

const product = numbers.reduce(function(total, num) {
    return total * num;
}, 1);
console.log(product); // 120

// Chaining methods
const result = numbers
    .filter(num => num > 2)      // [3, 4, 5]
    .map(num => num * 2)         // [6, 8, 10]
    .reduce((sum, num) => sum + num, 0); // 24

console.log(result); // 24
```

---

## 🎭 Function Expressions vs Declarations

### Hoisting Differences
```javascript
// Function declarations are hoisted
console.log(declaration()); // "I'm hoisted!"

function declaration() {
    return "I'm hoisted!";
}

// Function expressions are NOT hoisted
// console.log(expression()); // ❌ Error!

const expression = function() {
    return "I'm not hoisted!";
};

console.log(expression()); // "I'm not hoisted!"
```

### When to Use What
```javascript
// Use function declarations for:
// - Main functions you want available throughout the scope
// - Functions you might call before they're defined

function mainFunction() {
    return "Available everywhere in this scope";
}

// Use function expressions for:
// - Functions as values (callbacks, event handlers)
// - Conditional function creation
// - When you want to prevent hoisting

const conditionalFunction = condition => {
    if (condition) {
        return function() { return "Condition was true"; };
    } else {
        return function() { return "Condition was false"; };
    }
};

const myFunction = conditionalFunction(true);
console.log(myFunction()); // "Condition was true"
```

---

## 🔧 Error Handling in Functions

### Try-Catch in Functions
```javascript
function divideNumbers(a, b) {
    try {
        if (b === 0) {
            throw new Error("Division by zero is not allowed");
        }
        
        if (typeof a !== 'number' || typeof b !== 'number') {
            throw new Error("Both arguments must be numbers");
        }
        
        return a / b;
    } catch (error) {
        console.log("Error:", error.message);
        return null;
    }
}

console.log(divideNumbers(10, 2));    // 5
console.log(divideNumbers(10, 0));    // "Error: Division by zero..." then null
console.log(divideNumbers(10, "a"));  // "Error: Both arguments..." then null
```

### Input Validation
```javascript
function createUser(name, email, age) {
    // Input validation
    if (!name || typeof name !== 'string') {
        throw new Error("Name is required and must be a string");
    }
    
    if (!email || !email.includes('@')) {
        throw new Error("Valid email is required");
    }
    
    if (age < 0 || age > 150) {
        throw new Error("Age must be between 0 and 150");
    }
    
    return {
        name: name.trim(),
        email: email.toLowerCase().trim(),
        age: age,
        id: Date.now().toString()
    };
}

try {
    const user1 = createUser("Alice", "alice@email.com", 25);
    console.log(user1);
    
    const user2 = createUser("", "invalid-email", -5); // Will throw error
} catch (error) {
    console.log("Failed to create user:", error.message);
}
```

---

## 🎪 Practical Examples

### Example 1: Calculator
```javascript
const calculator = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => b !== 0 ? a / b : "Cannot divide by zero",
    
    calculate: function(operation, a, b) {
        if (this[operation]) {
            return this[operation](a, b);
        }
        return "Invalid operation";
    }
};

console.log(calculator.add(5, 3));                    // 8
console.log(calculator.calculate("multiply", 4, 7));  // 28
console.log(calculator.calculate("divide", 10, 0));   // "Cannot divide by zero"
```

### Example 2: Todo List Manager
```javascript
function createTodoManager() {
    let todos = [];
    let nextId = 1;
    
    return {
        addTodo: function(text) {
            const todo = {
                id: nextId++,
                text: text,
                completed: false,
                createdAt: new Date()
            };
            todos.push(todo);
            return todo;
        },
        
        getAllTodos: function() {
            return [...todos]; // Return copy to prevent external modification
        },
        
        getTodoById: function(id) {
            return todos.find(todo => todo.id === id);
        },
        
        completeTodo: function(id) {
            const todo = this.getTodoById(id);
            if (todo) {
                todo.completed = true;
                return todo;
            }
            return null;
        },
        
        deleteTodo: function(id) {
            const index = todos.findIndex(todo => todo.id === id);
            if (index !== -1) {
                return todos.splice(index, 1)[0];
            }
            return null;
        },
        
        filterTodos: function(filterFn) {
            return todos.filter(filterFn);
        },
        
        getStats: function() {
            const completed = todos.filter(todo => todo.completed).length;
            const pending = todos.length - completed;
            
            return {
                total: todos.length,
                completed: completed,
                pending: pending
            };
        }
    };
}

// Usage
const todoManager = createTodoManager();

todoManager.addTodo("Learn JavaScript");
todoManager.addTodo("Build a project");
todoManager.addTodo("Get a job");

console.log(todoManager.getAllTodos());

todoManager.completeTodo(1);
console.log(todoManager.getStats()); // {total: 3, completed: 1, pending: 2}

const pendingTodos = todoManager.filterTodos(todo => !todo.completed);
console.log(pendingTodos);
```

### Example 3: Utility Functions Library
```javascript
const utils = {
    // String utilities
    capitalize: str => str.charAt(0).toUpperCase() + str.slice(1).toLowerCase(),
    
    slugify: str => str.toLowerCase().replace(/\s+/g, '-').replace(/[^a-z0-9-]/g, ''),
    
    truncate: (str, length = 50) => {
        return str.length > length ? str.slice(0, length) + '...' : str;
    },
    
    // Array utilities
    shuffle: arr => {
        const shuffled = [...arr];
        for (let i = shuffled.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
        }
        return shuffled;
    },
    
    unique: arr => [...new Set(arr)],
    
    chunk: (arr, size) => {
        const chunks = [];
        for (let i = 0; i < arr.length; i += size) {
            chunks.push(arr.slice(i, i + size));
        }
        return chunks;
    },
    
    // Number utilities
    random: (min, max) => Math.floor(Math.random() * (max - min + 1)) + min,
    
    isEven: num => num % 2 === 0,
    
    clamp: (num, min, max) => Math.min(Math.max(num, min), max),
    
    // Object utilities
    pick: (obj, keys) => {
        const picked = {};
        keys.forEach(key => {
            if (key in obj) {
                picked[key] = obj[key];
            }
        });
        return picked;
    },
    
    omit: (obj, keys) => {
        const omitted = { ...obj };
        keys.forEach(key => delete omitted[key]);
        return omitted;
    }
};

// Usage examples
console.log(utils.capitalize("hello world"));           // "Hello world"
console.log(utils.slugify("Hello World! 123"));         // "hello-world-123"
console.log(utils.truncate("This is a very long string", 10)); // "This is a ..."

const numbers = [1, 2, 3, 4, 5];
console.log(utils.shuffle(numbers));                     // [3, 1, 5, 2, 4] (random)

const duplicates = [1, 2, 2, 3, 3, 3];
console.log(utils.unique(duplicates));                   // [1, 2, 3]

const longArray = [1, 2, 3, 4, 5, 6, 7, 8];
console.log(utils.chunk(longArray, 3));                  // [[1,2,3], [4,5,6], [7,8]]

console.log(utils.random(1, 10));                        // Random number between 1-10
console.log(utils.clamp(15, 1, 10));                     // 10 (clamped to max)

const person = { name: "Alice", age: 30, email: "alice@email.com", password: "secret" };
console.log(utils.pick(person, ["name", "email"]));      // {name: "Alice", email: "alice@email.com"}
console.log(utils.omit(person, ["password"]));           // {name: "Alice", age: 30, email: "alice@email.com"}
```

---

## 🚨 Common Mistakes to Avoid

### 1. Forgetting to Return
```javascript
// ❌ Wrong - function doesn't return anything
function addNumbers(a, b) {
    a + b; // This does nothing!
}

console.log(addNumbers(5, 3)); // undefined

// ✅ Correct
function addNumbers(a, b) {
    return a + b;
}

console.log(addNumbers(5, 3)); // 8
```

### 2. Arrow Functions and `this`
```javascript
// ❌ Wrong - arrow function doesn't have its own 'this'
const person = {
    name: "Alice",
    sayName: () => {
        console.log(this.name); // undefined or window.name
    }
};

// ✅ Correct - use regular function
const person = {
    name: "Alice",
    sayName: function() {
        console.log(this.name); // "Alice"
    }
};
```

### 3. Modifying Parameters
```javascript
// ❌ Wrong - modifying array parameter affects original
function doubleArray(arr) {
    for (let i = 0; i < arr.length; i++) {
        arr[i] *= 2; // Modifies original array!
    }
    return arr;
}

let numbers = [1, 2, 3];
let doubled = doubleArray(numbers);
console.log(numbers); // [2, 4, 6] - original changed!

// ✅ Correct - create new array
function doubleArray(arr) {
    return arr.map(num => num * 2);
}

let numbers = [1, 2, 3];
let doubled = doubleArray(numbers);
console.log(numbers); // [1, 2, 3] - original unchanged
console.log(doubled); // [2, 4, 6]
```

### 4. Not Handling Edge Cases
```javascript
// ❌ Wrong - doesn't handle edge cases
function getFirstElement(arr) {
    return arr[0];
}

console.log(getFirstElement([])); // undefined
console.log(getFirstElement(null)); // Error!

// ✅ Correct - handle edge cases
function getFirstElement(arr) {
    if (!Array.isArray(arr) || arr.length === 0) {
        return null;
    }
    return arr[0];
}

console.log(getFirstElement([]));    // null
console.log(getFirstElement(null));  // null
console.log(getFirstElement([1,2,3])); // 1
```

---

## 📋 Quick Reference Cheat Sheet

| Concept | Syntax | Use Case | Example |
|---------|--------|----------|---------|
| **Function Declaration** | `function name() {}` | Main functions, hoisted | `function greet() { return "Hello"; }` |
| **Function Expression** | `const name = function() {}` | Conditional creation, not hoisted | `const greet = function() { return "Hello"; };` |
| **Arrow Function** | `const name = () => {}` | Short functions, callbacks | `const add = (a, b) => a + b;` |
| **Parameters** | `function name(param1, param2)` | Function inputs | `function greet(name, age) {}` |
| **Default Parameters** | `function name(param = default)` | Optional parameters | `function greet(name = "Guest") {}` |
| **Rest Parameters** | `function name(...args)` | Variable arguments | `function sum(...numbers) {}` |
| **Return Statement** | `return value;` | Function output | `return name.toUpperCase();` |
| **IIFE** | `(function() {})()` | Immediate execution | `(function() { console.log("Now!"); })();` |
| **Callback** | `function(callback) { callback(); }` | Function as parameter | `setTimeout(callback, 1000);` |
| **Closure** | Inner function accessing outer scope | Data privacy | `function outer() { let x = 1; return () => x; }` |

### Function Best Practices ✅

1. **Use descriptive names**: `calculateTotalPrice()` not `calc()`
2. **Keep functions small**: One function, one responsibility
3. **Return early**: Use guard clauses to reduce nesting
4. **Handle edge cases**: Check for null, undefined, empty arrays
5. **Use pure functions when possible**: Same input = same output
6. **Comment complex functions**: Explain what, not how
7. **Validate inputs**: Check types and values
8. **Use consistent naming**: `getUserData()`, `setUserData()`

---

**🎉 Congratulations!** You now have a comprehensive understanding of JavaScript functions! Functions are the building blocks of JavaScript programming. Practice writing different types of functions, experiment with closures and higher-order functions, and always think about making your code readable and reusable.

Remember: **Functions are first-class citizens in JavaScript** - they can be stored in variables, passed as arguments, returned from other functions, and have properties and methods just like any other object! 🚀