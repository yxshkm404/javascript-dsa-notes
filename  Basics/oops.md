# JavaScript Object-Oriented Programming (OOP) - Complete Guide 📚

## What is Object-Oriented Programming?

Object-Oriented Programming (OOP) is a programming paradigm that organizes code using **objects** and **classes**. Think of it like organizing the real world - everything is an object with properties (characteristics) and methods (actions it can perform).

```javascript
// Real world example: A car is an object
const car = {
    // Properties (what it has)
    brand: "Toyota",
    color: "red",
    speed: 0,
    
    // Methods (what it can do)
    start: function() {
        console.log("Car is starting...");
    },
    accelerate: function() {
        this.speed += 10;
        console.log(`Speed is now ${this.speed} km/h`);
    }
};

car.start();        // "Car is starting..."
car.accelerate();   // "Speed is now 10 km/h"
```

### Why Use OOP?
- **Organization**: Code is structured and easier to understand
- **Reusability**: Create templates (classes) to make multiple objects
- **Maintainability**: Changes in one place affect related objects
- **Real-world modeling**: Mirrors how we think about real objects

---

## 🏗️ The Four Pillars of OOP

### 1. **Encapsulation** 📦
Bundling data and methods together, hiding internal details.

### 2. **Inheritance** 👨‍👩‍👧‍👦
Creating new classes based on existing ones.

### 3. **Polymorphism** 🎭
Same interface, different implementations.

### 4. **Abstraction** 🎨
Hiding complex implementation details, showing only necessary features.

---

## 🎯 Objects in JavaScript

### Creating Objects

#### 1. Object Literal (Simplest Way)
```javascript
const student = {
    name: "Alice",
    age: 20,
    grade: "A",
    
    study: function() {
        console.log(`${this.name} is studying...`);
    },
    
    getInfo: function() {
        return `${this.name}, age ${this.age}, grade ${this.grade}`;
    }
};

console.log(student.name);     // "Alice"
console.log(student.getInfo()); // "Alice, age 20, grade A"
student.study();               // "Alice is studying..."
```

#### 2. Object Constructor
```javascript
function Student(name, age, grade) {
    this.name = name;
    this.age = age;
    this.grade = grade;
    
    this.study = function() {
        console.log(`${this.name} is studying...`);
    };
    
    this.getInfo = function() {
        return `${this.name}, age ${this.age}, grade ${this.grade}`;
    };
}

const student1 = new Student("Bob", 19, "B+");
const student2 = new Student("Carol", 21, "A-");

console.log(student1.getInfo()); // "Bob, age 19, grade B+"
console.log(student2.getInfo()); // "Carol, age 21, grade A-"
```

#### 3. Object.create()
```javascript
const studentPrototype = {
    study: function() {
        console.log(`${this.name} is studying...`);
    },
    
    getInfo: function() {
        return `${this.name}, age ${this.age}, grade ${this.grade}`;
    }
};

const student = Object.create(studentPrototype);
student.name = "David";
student.age = 22;
student.grade = "A";

console.log(student.getInfo()); // "David, age 22, grade A"
```

---

## 🏛️ Classes (ES6+)

Classes provide a cleaner syntax for creating objects and handling inheritance.

### Basic Class Syntax
```javascript
class Animal {
    // Constructor method - runs when object is created
    constructor(name, species) {
        this.name = name;
        this.species = species;
    }
    
    // Methods
    speak() {
        console.log(`${this.name} makes a sound`);
    }
    
    getInfo() {
        return `${this.name} is a ${this.species}`;
    }
    
    // Static method - belongs to class, not instances
    static getKingdom() {
        return "Animalia";
    }
}

// Creating objects (instances)
const dog = new Animal("Buddy", "Dog");
const cat = new Animal("Whiskers", "Cat");

console.log(dog.getInfo());     // "Buddy is a Dog"
cat.speak();                    // "Whiskers makes a sound"
console.log(Animal.getKingdom()); // "Animalia"
```

### Class with Private Properties
```javascript
class BankAccount {
    // Private field (starts with #)
    #balance = 0;
    #accountNumber;
    
    constructor(accountNumber, initialBalance = 0) {
        this.#accountNumber = accountNumber;
        this.#balance = initialBalance;
        this.owner = "";
    }
    
    // Public method to access private data
    getBalance() {
        return this.#balance;
    }
    
    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
            console.log(`Deposited $${amount}. New balance: $${this.#balance}`);
        } else {
            console.log("Invalid deposit amount");
        }
    }
    
    withdraw(amount) {
        if (amount > 0 && amount <= this.#balance) {
            this.#balance -= amount;
            console.log(`Withdrew $${amount}. New balance: $${this.#balance}`);
        } else {
            console.log("Invalid withdrawal amount or insufficient funds");
        }
    }
    
    // Private method
    #validateTransaction(amount) {
        return amount > 0 && typeof amount === 'number';
    }
}

const account = new BankAccount("123456789", 1000);
account.deposit(500);           // "Deposited $500. New balance: $1500"
account.withdraw(200);          // "Withdrew $200. New balance: $1300"
console.log(account.getBalance()); // 1300

// console.log(account.#balance); // ❌ Error! Private field
```

---

## 🧬 Inheritance

Inheritance allows you to create new classes based on existing ones.

### Basic Inheritance
```javascript
// Parent class (Base class)
class Vehicle {
    constructor(brand, model, year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.speed = 0;
    }
    
    start() {
        console.log(`${this.brand} ${this.model} is starting...`);
    }
    
    stop() {
        this.speed = 0;
        console.log(`${this.brand} ${this.model} has stopped.`);
    }
    
    accelerate(increase) {
        this.speed += increase;
        console.log(`Speed increased to ${this.speed} km/h`);
    }
    
    getInfo() {
        return `${this.year} ${this.brand} ${this.model}`;
    }
}

// Child class (Derived class)
class Car extends Vehicle {
    constructor(brand, model, year, doors) {
        super(brand, model, year); // Call parent constructor
        this.doors = doors;
        this.type = "Car";
    }
    
    // Override parent method
    start() {
        console.log("Turning the key...");
        super.start(); // Call parent method
        console.log("Car is ready to drive!");
    }
    
    // New method specific to Car
    honk() {
        console.log("Beep beep! 🚗");
    }
    
    // Override parent method
    getInfo() {
        return `${super.getInfo()} with ${this.doors} doors`;
    }
}

class Motorcycle extends Vehicle {
    constructor(brand, model, year, engineSize) {
        super(brand, model, year);
        this.engineSize = engineSize;
        this.type = "Motorcycle";
    }
    
    start() {
        console.log("Kick starting...");
        super.start();
        console.log("Ready to ride! 🏍️");
    }
    
    wheelie() {
        console.log("Doing a wheelie! 🤸‍♂️");
    }
}

// Usage
const myCar = new Car("Honda", "Civic", 2022, 4);
const myBike = new Motorcycle("Harley", "Davidson", 2021, 1200);

myCar.start();
// Output:
// "Turning the key..."
// "Honda Civic is starting..."
// "Car is ready to drive!"

myBike.start();
// Output:
// "Kick starting..."
// "Harley Davidson is starting..."
// "Ready to ride! 🏍️"

myCar.honk();       // "Beep beep! 🚗"
myBike.wheelie();   // "Doing a wheelie! 🤸‍♂️"

console.log(myCar.getInfo());  // "2022 Honda Civic with 4 doors"
```

### Multi-level Inheritance
```javascript
class LivingBeing {
    constructor(name) {
        this.name = name;
        this.alive = true;
    }
    
    breathe() {
        console.log(`${this.name} is breathing`);
    }
}

class Animal extends LivingBeing {
    constructor(name, species) {
        super(name);
        this.species = species;
    }
    
    move() {
        console.log(`${this.name} is moving`);
    }
}

class Mammal extends Animal {
    constructor(name, species, furColor) {
        super(name, species);
        this.furColor = furColor;
        this.warmBlooded = true;
    }
    
    feedMilk() {
        console.log(`${this.name} is feeding milk to babies`);
    }
}

class Dog extends Mammal {
    constructor(name, breed, furColor) {
        super(name, "Dog", furColor);
        this.breed = breed;
    }
    
    bark() {
        console.log(`${this.name} says: Woof! 🐕`);
    }
    
    wagTail() {
        console.log(`${this.name} is wagging tail happily!`);
    }
}

const myDog = new Dog("Max", "Golden Retriever", "Golden");

myDog.breathe();    // From LivingBeing
myDog.move();       // From Animal  
myDog.feedMilk();   // From Mammal
myDog.bark();       // From Dog
myDog.wagTail();    // From Dog

console.log(myDog.name);         // "Max"
console.log(myDog.species);      // "Dog"
console.log(myDog.breed);        // "Golden Retriever"
console.log(myDog.warmBlooded);  // true
```

---

## 🎭 Polymorphism

Polymorphism allows objects of different classes to be treated the same way through a common interface.

### Method Overriding
```javascript
class Shape {
    constructor(color) {
        this.color = color;
    }
    
    area() {
        return 0; // Default implementation
    }
    
    describe() {
        console.log(`This is a ${this.color} shape with area ${this.area()}`);
    }
}

class Circle extends Shape {
    constructor(color, radius) {
        super(color);
        this.radius = radius;
    }
    
    // Override area method
    area() {
        return Math.PI * this.radius * this.radius;
    }
}

class Rectangle extends Shape {
    constructor(color, width, height) {
        super(color);
        this.width = width;
        this.height = height;
    }
    
    // Override area method
    area() {
        return this.width * this.height;
    }
}

class Triangle extends Shape {
    constructor(color, base, height) {
        super(color);
        this.base = base;
        this.height = height;
    }
    
    // Override area method
    area() {
        return 0.5 * this.base * this.height;
    }
}

// Polymorphism in action
const shapes = [
    new Circle("red", 5),
    new Rectangle("blue", 4, 6),
    new Triangle("green", 8, 3)
];

shapes.forEach(shape => {
    shape.describe();
    // Each shape calculates area differently but uses same interface
});

// Output:
// "This is a red shape with area 78.54"
// "This is a blue shape with area 24"
// "This is a green shape with area 12"
```

### Duck Typing
```javascript
// If it looks like a duck and quacks like a duck, it's a duck
class Duck {
    speak() {
        return "Quack!";
    }
    
    fly() {
        return "Flying like a duck";
    }
}

class Robot {
    speak() {
        return "Beep boop!";
    }
    
    fly() {
        return "Flying with rockets";
    }
}

class Airplane {
    speak() {
        return "Engine noise";
    }
    
    fly() {
        return "Flying with wings";
    }
}

// Function that works with any object that has speak() and fly() methods
function makeItFly(flyingThing) {
    console.log(flyingThing.speak());
    console.log(flyingThing.fly());
    console.log("---");
}

const duck = new Duck();
const robot = new Robot();
const plane = new Airplane();

makeItFly(duck);   // Works!
makeItFly(robot);  // Works!
makeItFly(plane);  // Works!
```

---

## 📦 Encapsulation

Encapsulation is about bundling data and methods together and controlling access to them.

### Using Getters and Setters
```javascript
class Person {
    constructor(firstName, lastName, age) {
        this._firstName = firstName;  // Convention: _ means private
        this._lastName = lastName;
        this._age = age;
    }
    
    // Getter for full name
    get fullName() {
        return `${this._firstName} ${this._lastName}`;
    }
    
    // Setter for full name
    set fullName(name) {
        const parts = name.split(' ');
        this._firstName = parts[0] || '';
        this._lastName = parts[1] || '';
    }
    
    // Getter with validation
    get age() {
        return this._age;
    }
    
    // Setter with validation
    set age(newAge) {
        if (newAge >= 0 && newAge <= 150) {
            this._age = newAge;
        } else {
            console.log("Invalid age!");
        }
    }
    
    // Method
    introduce() {
        return `Hi, I'm ${this.fullName} and I'm ${this.age} years old.`;
    }
}

const person = new Person("John", "Doe", 30);

console.log(person.fullName);    // "John Doe" (using getter)
console.log(person.age);         // 30 (using getter)

person.fullName = "Jane Smith";  // Using setter
console.log(person.fullName);    // "Jane Smith"

person.age = 25;                 // Using setter
console.log(person.age);         // 25

person.age = -5;                 // "Invalid age!" (validation)
console.log(person.age);         // Still 25

console.log(person.introduce()); // "Hi, I'm Jane Smith and I'm 25 years old."
```

### Private Fields (Modern JavaScript)
```javascript
class CreditCard {
    #cardNumber;        // Private field
    #cvv;              // Private field
    #balance = 0;      // Private field with default value
    
    constructor(cardNumber, cvv, initialBalance = 0) {
        this.#cardNumber = cardNumber;
        this.#cvv = cvv;
        this.#balance = initialBalance;
        this.holderName = "";  // Public field
    }
    
    // Public method to access private data
    getMaskedCardNumber() {
        const visible = this.#cardNumber.slice(-4);
        return `****-****-****-${visible}`;
    }
    
    // Private method
    #validatePin(pin) {
        return pin === "1234"; // Simplified validation
    }
    
    // Public methods
    checkBalance(pin) {
        if (this.#validatePin(pin)) {
            return this.#balance;
        }
        return "Invalid PIN";
    }
    
    withdraw(amount, pin) {
        if (!this.#validatePin(pin)) {
            return "Invalid PIN";
        }
        
        if (amount > this.#balance) {
            return "Insufficient funds";
        }
        
        this.#balance -= amount;
        return `Withdrew $${amount}. New balance: $${this.#balance}`;
    }
    
    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
            return `Deposited $${amount}. New balance: $${this.#balance}`;
        }
        return "Invalid amount";
    }
}

const card = new CreditCard("1234567890123456", "123", 1000);
card.holderName = "Alice Johnson";

console.log(card.getMaskedCardNumber()); // "****-****-****-3456"
console.log(card.checkBalance("1234"));  // 1000
console.log(card.withdraw(200, "1234")); // "Withdrew $200. New balance: $800"

// console.log(card.#balance);           // ❌ Error! Private field
// console.log(card.#validatePin("1234")); // ❌ Error! Private method
```

---

## 🎨 Abstraction

Abstraction hides complex implementation details and shows only essential features.

### Abstract Base Classes
```javascript
// Abstract class (not meant to be instantiated directly)
class DatabaseConnection {
    constructor(connectionString) {
        if (this.constructor === DatabaseConnection) {
            throw new Error("Cannot instantiate abstract class");
        }
        this.connectionString = connectionString;
        this.isConnected = false;
    }
    
    // Abstract methods (must be implemented by subclasses)
    connect() {
        throw new Error("connect() method must be implemented");
    }
    
    disconnect() {
        throw new Error("disconnect() method must be implemented");
    }
    
    query(sql) {
        throw new Error("query() method must be implemented");
    }
    
    // Concrete method (can be used by subclasses)
    getConnectionStatus() {
        return this.isConnected ? "Connected" : "Disconnected";
    }
}

class MySQLConnection extends DatabaseConnection {
    connect() {
        console.log("Connecting to MySQL database...");
        this.isConnected = true;
        return "MySQL connected successfully";
    }
    
    disconnect() {
        console.log("Disconnecting from MySQL database...");
        this.isConnected = false;
        return "MySQL disconnected successfully";
    }
    
    query(sql) {
        if (!this.isConnected) {
            return "Not connected to database";
        }
        return `Executing MySQL query: ${sql}`;
    }
}

class PostgreSQLConnection extends DatabaseConnection {
    connect() {
        console.log("Connecting to PostgreSQL database...");
        this.isConnected = true;
        return "PostgreSQL connected successfully";
    }
    
    disconnect() {
        console.log("Disconnecting from PostgreSQL database...");
        this.isConnected = false;
        return "PostgreSQL disconnected successfully";
    }
    
    query(sql) {
        if (!this.isConnected) {
            return "Not connected to database";
        }
        return `Executing PostgreSQL query: ${sql}`;
    }
}

// Usage
// const db = new DatabaseConnection("connection"); // ❌ Error! Abstract class

const mysqlDb = new MySQLConnection("mysql://localhost:3306");
const postgresDb = new PostgreSQLConnection("postgres://localhost:5432");

console.log(mysqlDb.connect());           // MySQL connects
console.log(mysqlDb.query("SELECT * FROM users")); // MySQL query

console.log(postgresDb.connect());        // PostgreSQL connects
console.log(postgresDb.query("SELECT * FROM products")); // PostgreSQL query
```

### Interface Pattern
```javascript
// Interface-like pattern using classes
class PaymentProcessor {
    processPayment(amount) {
        throw new Error("processPayment method must be implemented");
    }
    
    refund(transactionId) {
        throw new Error("refund method must be implemented");
    }
}

class CreditCardProcessor extends PaymentProcessor {
    processPayment(amount) {
        console.log(`Processing credit card payment of $${amount}`);
        // Credit card specific logic
        return {
            success: true,
            transactionId: `cc_${Date.now()}`,
            amount: amount
        };
    }
    
    refund(transactionId) {
        console.log(`Refunding credit card transaction: ${transactionId}`);
        return { success: true, refunded: true };
    }
}

class PayPalProcessor extends PaymentProcessor {
    processPayment(amount) {
        console.log(`Processing PayPal payment of $${amount}`);
        // PayPal specific logic
        return {
            success: true,
            transactionId: `pp_${Date.now()}`,
            amount: amount
        };
    }
    
    refund(transactionId) {
        console.log(`Refunding PayPal transaction: ${transactionId}`);
        return { success: true, refunded: true };
    }
}

class BitcoinProcessor extends PaymentProcessor {
    processPayment(amount) {
        console.log(`Processing Bitcoin payment of $${amount}`);
        // Bitcoin specific logic
        return {
            success: true,
            transactionId: `btc_${Date.now()}`,
            amount: amount
        };
    }
    
    refund(transactionId) {
        console.log(`Bitcoin refunds are not supported: ${transactionId}`);
        return { success: false, refunded: false };
    }
}

// Payment service that works with any processor
class PaymentService {
    constructor(processor) {
        this.processor = processor;
    }
    
    makePayment(amount) {
        console.log(`Making payment of $${amount}...`);
        return this.processor.processPayment(amount);
    }
    
    processRefund(transactionId) {
        console.log(`Processing refund for ${transactionId}...`);
        return this.processor.refund(transactionId);
    }
}

// Usage - same interface, different implementations
const creditCardService = new PaymentService(new CreditCardProcessor());
const paypalService = new PaymentService(new PayPalProcessor());
const bitcoinService = new PaymentService(new BitcoinProcessor());

const transaction1 = creditCardService.makePayment(100);
const transaction2 = paypalService.makePayment(50);
const transaction3 = bitcoinService.makePayment(75);

creditCardService.processRefund(transaction1.transactionId);
bitcoinService.processRefund(transaction3.transactionId);
```

---

## 🔧 Advanced OOP Concepts

### Mixins
Mixins allow you to add functionality to classes without inheritance.

```javascript
// Mixin for flying ability
const FlyingMixin = {
    fly() {
        console.log(`${this.name} is flying! ✈️`);
    },
    
    land() {
        console.log(`${this.name} is landing! 🛬`);
    }
};

// Mixin for swimming ability  
const SwimmingMixin = {
    swim() {
        console.log(`${this.name} is swimming! 🏊‍♂️`);
    },
    
    dive() {
        console.log(`${this.name} is diving deep! 🤿`);
    }
};

// Function to apply mixins to a class
function applyMixins(targetClass, ...mixins) {
    mixins.forEach(mixin => {
        Object.getOwnPropertyNames(mixin).forEach(name => {
            if (name !== 'constructor') {
                targetClass.prototype[name] = mixin[name];
            }
        });
    });
}

class Bird {
    constructor(name, species) {
        this.name = name;
        this.species = species;
    }
    
    chirp() {
        console.log(`${this.name} is chirping! 🐦`);
    }
}

class Fish {
    constructor(name, species) {
        this.name = name;
        this.species = species;
    }
}

class Duck extends Bird {
    constructor(name) {
        super(name, "Duck");
    }
}

// Apply mixins
applyMixins(Bird, FlyingMixin);
applyMixins(Fish, SwimmingMixin);
applyMixins(Duck, SwimmingMixin); // Ducks can also swim!

// Usage
const eagle = new Bird("Eagle", "Bald Eagle");
const salmon = new Fish("Salmon", "Atlantic Salmon");
const duck = new Duck("Donald");

eagle.chirp();  // "Eagle is chirping! 🐦"
eagle.fly();    // "Eagle is flying! ✈️"

salmon.swim();  // "Salmon is swimming! 🏊‍♂️"
salmon.dive();  // "Salmon is diving deep! 🤿"

duck.chirp();   // "Donald is chirping! 🐦"
duck.fly();     // "Donald is flying! ✈️"
duck.swim();    // "Donald is swimming! 🏊‍♂️"
```

### Composition over Inheritance
```javascript
// Instead of deep inheritance, use composition
class Engine {
    constructor(type, power) {
        this.type = type;
        this.power = power;
        this.running = false;
    }
    
    start() {
        this.running = true;
        console.log(`${this.type} engine started (${this.power}HP)`);
    }
    
    stop() {
        this.running = false;
        console.log(`${this.type} engine stopped`);
    }
}

class GPS {
    constructor() {
        this.currentLocation = "Unknown";
    }
    
    navigate(destination) {
        console.log(`Navigating to ${destination} from ${this.currentLocation}`);
    }
    
    updateLocation(location) {
        this.currentLocation = location;
    }
}

class Radio {
    constructor() {
        this.station = "FM 100.1";
        this.volume = 5;
    }
    
    tune(station) {
        this.station = station;
        console.log(`Tuned to ${station}`);
    }
    
    adjustVolume(level) {
        this.volume = level;
        console.log(`Volume set to ${level}`);
    }
}

// Car uses composition instead of inheritance
class Car {
    constructor(brand, model) {
        this.brand = brand;
        this.model = model;
        
        // Compose with other objects
        this.engine = new Engine("V6", 300);
        this.gps = new GPS();
        this.radio = new Radio();
    }
    
    start() {
        console.log(`Starting ${this.brand} ${this.model}...`);
        this.engine.start();
    }
    
    stop() {
        this.engine.stop();
        console.log(`${this.brand} ${this.model} stopped.`);
    }
    
    // Delegate to composed objects
    navigate(destination) {
        this.gps.navigate(destination);
    }
    
    playMusic(station) {
        this.radio.tune(station);
    }
}

const myCar = new Car("Toyota", "Camry");
myCar.start();                    // Uses engine
myCar.navigate("New York");       // Uses GPS
myCar.playMusic("Classic Rock FM"); // Uses radio
myCar.stop();                     // Uses engine
```

---

## 🎯 Prototype-based Programming

JavaScript uses prototypes for inheritance. Understanding this helps you understand how classes work under the hood.

### Prototype Chain
```javascript
// Constructor function (pre-ES6 way)
function Animal(name, species) {
    this.name = name;
    this.species = species;
}

// Adding methods to prototype
Animal.prototype.speak = function() {
    console.log(`${this.name} makes a sound`);
};

Animal.prototype.getInfo = function() {
    return `${this.name} is a ${this.species}`;
};

// Create instances
const dog = new Animal("Buddy", "Dog");
const cat = new Animal("Whiskers", "Cat");

dog.speak();                    // "Buddy makes a sound"
console.log(cat.getInfo());     // "Whiskers is a Cat"

// All instances share the same methods
console.log(dog.speak === cat.speak); // true

// Prototype inheritance
function Dog(name, breed) {
    Animal.call(this, name, "Dog"); // Call parent constructor
    this.breed = breed;
}

// Set up inheritance
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// Add Dog-specific methods
Dog.prototype.bark = function() {
    console.log(`${this.name} barks: Woof!`);
};

// Override parent method
Dog.prototype.speak = function() {
    this.bark();
};

const goldenRetriever = new Dog("Max", "Golden Retriever");
goldenRetriever.speak();        // "Max barks: Woof!"
console.log(goldenRetriever.getInfo()); // "Max is a Dog"
```

### Understanding `__proto__` and `prototype`
```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    return `Hello, I'm ${this.name}`;
};

const alice = new Person("Alice");

// Understanding the prototype chain
console.log(alice.__proto__ === Person.prototype);           // true
console.log(Person.prototype.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__);                     // null

// Adding methods dynamically
Person.prototype.sayGoodbye = function() {
    return `Goodbye from ${this.name}`;
};

console.log(alice.sayGoodbye()); // "Goodbye from Alice" - works on existing instances!

// Prototype chain lookup
console.log(alice.hasOwnProperty('name'));    // true (own property)
console.log(alice.hasOwnProperty('greet'));   // false (inherited)
```

---

## 🎪 Real-World Examples

### Example 1: E-commerce System
```javascript
// Base Product class
class Product {
    constructor(name, price, category) {
        this.name = name;
        this.price = price;
        this.category = category;
        this.id = this.generateId();
    }
    
    generateId() {
        return Math.random().toString(36).substr(2, 9);
    }
    
    getDisplayPrice() {
        return `$${this.price.toFixed(2)}`;
    }
    
    getInfo() {
        return `${this.name} - ${this.getDisplayPrice()}`;
    }
    
    applyDiscount(percentage) {
        this.price *= (1 - percentage / 100);
        console.log(`Applied ${percentage}% discount to ${this.name}`);
    }
}

// Specific product types
class Electronics extends Product {
    constructor(name, price, brand, warranty) {
        super(name, price, "Electronics");
        this.brand = brand;
        this.warranty = warranty;
    }
    
    getInfo() {
        return `${super.getInfo()} by ${this.brand} (${this.warranty} warranty)`;
    }
}

class Clothing extends Product {
    constructor(name, price, size, color) {
        super(name, price, "Clothing");
        this.size = size;
        this.color = color;
    }
    
    getInfo() {
        return `${super.getInfo()} - Size: ${this.size}, Color: ${this.color}`;
    }
}

// Shopping Cart
class ShoppingCart {
    constructor() {
        this.items = [];
    }
    
    addItem(product, quantity = 1) {
        const existingItem = this.items.find(item => item.product.id === product.id);
        
        if (existingItem) {
            existingItem.quantity += quantity;
        } else {
            this.items.push({ product, quantity });
        }
        
        console.log(`Added ${quantity}x ${product.name} to cart`);
    }
    
    removeItem(productId) {
        const index = this.items.findIndex(item => item.product.id === productId);
        if (index !== -1) {
            const removed = this.items.splice(index, 1)[0];
            console.log(`Removed ${removed.product.name} from cart`);
        }
    }
    
    getTotal() {
        return this.items.reduce((total, item) => {
            return total + (item.product.price * item.quantity);
        }, 0);
    }
    
    displayCart() {
        console.log("\n--- Shopping Cart ---");
        this.items.forEach(item => {
            console.log(`${item.quantity}x ${item.product.getInfo()} = $${(item.product.price * item.quantity).toFixed(2)}`);
        });
        console.log(`\nTotal: $${this.getTotal().toFixed(2)}`);
    }
    
    checkout() {
        if (this.items.length === 0) {
            console.log("Cart is empty!");
            return;
        }
        
        console.log(`\nProcessing payment of $${this.getTotal().toFixed(2)}...`);
        console.log("Order confirmed! 🎉");
        this.items = []; // Clear cart
    }
}

// Usage
const laptop = new Electronics("Gaming Laptop", 1200, "ASUS", "2 years");
const tshirt = new Clothing("Cotton T-Shirt", 25, "L", "Blue");
const headphones = new Electronics("Wireless Headphones", 150, "Sony", "1 year");

const cart = new ShoppingCart();

cart.addItem(laptop);
cart.addItem(tshirt, 2);
cart.addItem(headphones);

// Apply discount
laptop.applyDiscount(10); // 10% off

cart.displayCart();
cart.checkout();
```

### Example 2: Game Character System
```javascript
// Base Character class
class Character {
    constructor(name, health = 100) {
        this.name = name;
        this.maxHealth = health;
        this.health = health;
        this.level = 1;
        this.experience = 0;
        this.alive = true;
    }
    
    takeDamage(damage) {
        if (!this.alive) return;
        
        this.health -= damage;
        console.log(`${this.name} takes ${damage} damage! Health: ${this.health}/${this.maxHealth}`);
        
        if (this.health <= 0) {
            this.health = 0;
            this.alive = false;
            console.log(`${this.name} has been defeated! ☠️`);
        }
    }
    
    heal(amount) {
        if (!this.alive) return;
        
        this.health = Math.min(this.health + amount, this.maxHealth);
        console.log(`${this.name} heals for ${amount}! Health: ${this.health}/${this.maxHealth}`);
    }
    
    gainExperience(exp) {
        this.experience += exp;
        console.log(`${this.name} gains ${exp} experience!`);
        
        // Level up every 100 exp
        const newLevel = Math.floor(this.experience / 100) + 1;
        if (newLevel > this.level) {
            this.levelUp(newLevel);
        }
    }
    
    levelUp(newLevel) {
        this.level = newLevel;
        this.maxHealth += 20;
        this.health = this.maxHealth; // Full heal on level up
        console.log(`🎉 ${this.name} leveled up to level ${this.level}! Max health increased!`);
    }
    
    getStatus() {
        const status = this.alive ? "Alive" : "Defeated";
        return `${this.name} (Level ${this.level}) - ${status} - HP: ${this.health}/${this.maxHealth}`;
    }
}

// Warrior class
class Warrior extends Character {
    constructor(name) {
        super(name, 120); // More health
        this.attackPower = 25;
        this.armor = 5;
    }
    
    attack(target) {
        if (!this.alive) return;
        
        console.log(`${this.name} attacks ${target.name} with a sword! ⚔️`);
        target.takeDamage(this.attackPower);
        
        if (!target.alive) {
            this.gainExperience(50);
        }
    }
    
    defend() {
        console.log(`${this.name} raises shield! Defense increased temporarily! 🛡️`);
        this.armor += 3;
        
        // Reset armor after some time (simplified)
        setTimeout(() => {
            this.armor -= 3;
            console.log(`${this.name}'s defense returns to normal.`);
        }, 3000);
    }
    
    takeDamage(damage) {
        const actualDamage = Math.max(damage - this.armor, 0);
        super.takeDamage(actualDamage);
    }
}

// Mage class
class Mage extends Character {
    constructor(name) {
        super(name, 80); // Less health
        this.mana = 100;
        this.maxMana = 100;
        this.spellPower = 30;
    }
    
    castSpell(target, spellName = "Fireball") {
        if (!this.alive) return;
        
        if (this.mana < 20) {
            console.log(`${this.name} doesn't have enough mana!`);
            return;
        }
        
        this.mana -= 20;
        console.log(`${this.name} casts ${spellName}!