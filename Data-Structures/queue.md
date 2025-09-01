# Queue Data Structure

## What is a Queue?

A **Queue** is a linear data structure that follows the **FIFO (First In, First Out)** principle. Think of it like a line of people waiting at a ticket counter - the first person in line is the first one to be served.

![Queue Visualization](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/600px-Data_Queue.svg.png)

### Key Characteristics:
- Elements are added at the **rear** (back) of the queue
- Elements are removed from the **front** of the queue
- Access is restricted to the front and rear ends only

## Queue Operations

### Basic Operations:

| Operation | Description | Visual |
|-----------|-------------|--------|
| **Enqueue** | Add element to the rear | `[1, 2, 3] → enqueue(4) → [1, 2, 3, 4]` |
| **Dequeue** | Remove element from front | `[1, 2, 3, 4] → dequeue() → [2, 3, 4] (returns 1)` |
| **Peek/Front** | View front element without removing | `[1, 2, 3] → peek() → returns 1` |
| **isEmpty** | Check if queue is empty | `[] → isEmpty() → true` |
| **Size** | Get number of elements | `[1, 2, 3] → size() → 3` |

## Types of Queues

### 1. Simple Queue (Linear Queue)
Basic implementation using arrays with `push()` and `shift()` methods.

### 2. Optimized Queue
Uses front and rear pointers to avoid shifting elements.

![Optimized Queue](https://media.geeksforgeeks.org/wp-content/uploads/20220805131014/fifo.png)

### 3. Circular Queue
Fixed-size queue where the rear connects back to the front when it reaches the end.

![Circular Queue](https://media.geeksforgeeks.org/wp-content/uploads/20220816162225/Queue.png)

## Implementation Examples

### 1. Simple Queue Implementation

```javascript
class Queue {
  constructor(){
    this.items = [];
  }
  
  // Add element to rear
  enqueue(element){
    this.items.push(element);
  }
  
  // Remove element from front
  dequeue(){
    return this.items.shift();
  }
  
  // Check if queue is empty
  isEmpty(){
    return this.items.length == 0;
  }
  
  // View front element (Note: should be 'peek', not 'peak')
  peek(){
    if(!this.isEmpty()){
      return this.items[0];
    }
    return null;
  }
  
  // Get queue size
  size(){
    return this.items.length;
  }
  
  // Display queue contents
  print(){
    console.log(this.items.toString());
  }

  // Iterator for queue - returns elements from front to rear
  *[Symbol.iterator](){
    for(let i = 0; i < this.items.length; i++){
      yield this.items[i];
    }
  }
  
  // Alternative iteration method
  forEach(callback){
    for(let i = 0; i < this.items.length; i++){
      callback(this.items[i], i);
    }
  }
}

// Usage Example
const queue = new Queue();
console.log(queue.isEmpty()); // true
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);
console.log(queue.size()); // 3
queue.print(); // "10,20,30"

// Iteration examples
console.log("Using for...of loop:");
for(const item of queue){
  console.log(item); // 10, 20, 30
}

console.log("Using forEach:");
queue.forEach((item, index) => {
  console.log(`Index: ${index}, Value: ${item}`);
});

console.log(queue.dequeue()); // 10
console.log(queue.peek()); // 20
```

**Issue with Simple Queue**: The `shift()` method has O(n) time complexity as it needs to shift all remaining elements.

### 2. Optimized Queue Implementation

![Optimized Queue Structure](https://media.geeksforgeeks.org/wp-content/uploads/20221213111946/1-660x330.png)

The optimized queue uses front and rear pointers to track positions without shifting elements:

![Optimized Queue Operations](https://prepinsta.com/wp-content/uploads/2020/12/Queue-using-Linked-List-in-C.webp)

```javascript
class OptimizedQueue{
  constructor(){
    this.items = {};
    this.rear = 0;
    this.front = 0;
  }
  
  // Add element at rear position
  enqueue(element){
    this.items[this.rear] = element;
    this.rear++;
  }
  
  // Remove element from front position
  dequeue(){
    const item = this.items[this.front];
    delete this.items[this.front];
    this.front++;
    return item;
  }
  
  // Check if queue is empty
  isEmpty(){
    return this.rear - this.front === 0;
  }
  
  // View front element
  peek(){
    return this.items[this.front];
  }
  
  // Calculate current size
  size(){
    return this.rear - this.front;
  }
  
  // Display queue
  print(){
    console.log(this.items);
  }

  // Iterator for optimized queue - iterates from front to rear
  *[Symbol.iterator](){
    for(let i = this.front; i < this.rear; i++){
      yield this.items[i];
    }
  }
  
  // Alternative iteration method
  forEach(callback){
    let index = 0;
    for(let i = this.front; i < this.rear; i++){
      callback(this.items[i], index);
      index++;
    }
  }

  // Get all values as array (useful for debugging)
  toArray(){
    const result = [];
    for(let i = this.front; i < this.rear; i++){
      result.push(this.items[i]);
    }
    return result;
  }
}

// Usage Example
const queue1 = new OptimizedQueue();
console.log(queue1.isEmpty()); // true
queue1.enqueue(10);
queue1.enqueue(20);
queue1.enqueue(30);
console.log(queue1.size()); // 3
queue1.print(); // {0: 10, 1: 20, 2: 30}

// Iteration examples
console.log("Iterating through optimized queue:");
for(const item of queue1){
  console.log(item); // 10, 20, 30
}

console.log("Using forEach on optimized queue:");
queue1.forEach((item, index) => {
  console.log(`Position: ${index}, Value: ${item}`);
});

console.log("Queue as array:", queue1.toArray()); // [10, 20, 30]

console.log(queue1.dequeue()); // 10
console.log(queue1.peek()); // 20
```

### 3. Circular Queue Implementation

![Circular Queue Concept](https://media.geeksforgeeks.org/wp-content/uploads/20220816162225/Queue.png)

A circular queue efficiently utilizes memory by connecting the end back to the beginning:

![Circular Queue Operations](https://static.javatpoint.com/ds/images/circular-queue.png)

Here's how circular queue operations work:

![Circular Queue Enqueue Dequeue](https://www.tutorialspoint.com/data_structures_algorithms/images/circular_queue_concept.jpg)

```javascript
class CircularQueue{
  constructor(capacity){
    this.items = new Array(capacity);
    this.capacity = capacity;
    this.currentLength = 0;
    this.rear = -1;
    this.front = -1;
  }
  
  // Check if queue is full
  isFull(){
    return this.currentLength === this.capacity;
  }
  
  // Check if queue is empty
  isEmpty(){
    return this.currentLength === 0;
  }
  
  // Add element (if not full)
  enqueue(element){
    if(!this.isFull()){
      this.rear = (this.rear + 1) % this.capacity;
      this.items[this.rear] = element;
      this.currentLength += 1;
      if(this.front === -1){
        this.front = this.rear;
      }
    }
  }
  
  // Remove element from front
  dequeue(){
    if(this.isEmpty()){
      return null;
    }
    const item = this.items[this.front];
    this.items[this.front] = null;
    this.front = (this.front + 1) % this.capacity;
    this.currentLength -= 1;
    if(this.isEmpty()){
      this.front = -1;
      this.rear = -1;
    }
    return item;
  }
  
  // View front element
  peek(){
    if(!this.isEmpty()){
      return this.items[this.front];
    }
  }
  
  // Display queue contents
  print(){
    if(this.isEmpty()){
      console.log('Queue is empty');
    } else {
      let i;
      let str = '';
      for(i = this.front; i !== this.rear; i = (i + 1) % this.capacity){
        str += this.items[i] + ' ';
      }
      str += this.items[i];
      console.log(str);
    }
  }

  // Iterator for circular queue - handles wraparound
  *[Symbol.iterator](){
    if(this.isEmpty()) return;
    
    let count = 0;
    let index = this.front;
    
    while(count < this.currentLength){
      yield this.items[index];
      index = (index + 1) % this.capacity;
      count++;
    }
  }
  
  // Alternative iteration method for circular queue
  forEach(callback){
    if(this.isEmpty()) return;
    
    let count = 0;
    let index = this.front;
    
    while(count < this.currentLength){
      callback(this.items[index], count);
      index = (index + 1) % this.capacity;
      count++;
    }
  }

  // Get all values as array (respects circular nature)
  toArray(){
    if(this.isEmpty()) return [];
    
    const result = [];
    let count = 0;
    let index = this.front;
    
    while(count < this.currentLength){
      result.push(this.items[index]);
      index = (index + 1) % this.capacity;
      count++;
    }
    return result;
  }

  // Advanced iteration: iterate with position info
  *entries(){
    if(this.isEmpty()) return;
    
    let count = 0;
    let index = this.front;
    
    while(count < this.currentLength){
      yield [count, this.items[index], index]; // [logical_position, value, physical_index]
      index = (index + 1) % this.capacity;
      count++;
    }
  }
}

// Usage Example
const circularQueue = new CircularQueue(5);
console.log(circularQueue.isEmpty()); // true
circularQueue.enqueue(10);
circularQueue.enqueue(20);
circularQueue.enqueue(30);
circularQueue.enqueue(40);
circularQueue.enqueue(50);
console.log(circularQueue.isFull()); // true
circularQueue.print(); // "10 20 30 40 50"

// Iteration examples for circular queue
console.log("\n=== Circular Queue Iteration Examples ===");

console.log("Using for...of loop:");
for(const item of circularQueue){
  console.log(item); // 10, 20, 30, 40, 50
}

console.log("Using forEach:");
circularQueue.forEach((item, position) => {
  console.log(`Position: ${position}, Value: ${item}`);
});

console.log("Queue as array:", circularQueue.toArray()); // [10, 20, 30, 40, 50]

// Demonstrate circular behavior
console.log("\n=== Testing Circular Behavior ===");
console.log("Dequeue two elements:");
console.log(circularQueue.dequeue()); // 10
console.log(circularQueue.dequeue()); // 20

console.log("Add new elements:");
circularQueue.enqueue(60);
circularQueue.enqueue(70);

console.log("Current queue after wraparound:");
for(const item of circularQueue){
  console.log(item); // 30, 40, 50, 60, 70
}

console.log("Using entries() to see logical vs physical positions:");
for(const [logicalPos, value, physicalIndex] of circularQueue.entries()){
  console.log(`Logical: ${logicalPos}, Value: ${value}, Physical Index: ${physicalIndex}`);
}
```

## Queue Iteration Explained

### Why Iteration Matters in Queues

While queues are primarily designed for FIFO access, iteration is useful for:
- **Debugging**: Viewing all elements without modifying the queue
- **Display**: Showing queue contents to users
- **Processing**: Applying operations to all elements
- **Conversion**: Converting queue to other data structures

### Iteration Patterns

#### 1. Simple Queue Iteration
```javascript
// Standard array iteration - straightforward
for(let i = 0; i < queue.items.length; i++){
  console.log(queue.items[i]);
}
```

#### 2. Optimized Queue Iteration
```javascript
// Iterate from front to rear using pointers
for(let i = queue.front; i < queue.rear; i++){
  console.log(queue.items[i]);
}
```

#### 3. Circular Queue Iteration (Key Concept)
```javascript
// Handle wraparound using modular arithmetic
let index = this.front;
for(let count = 0; count < this.currentLength; count++){
  console.log(this.items[index]);
  index = (index + 1) % this.capacity; // Wraparound logic
}
```

### Circular Queue Iteration Visualization

```
Circular Queue with capacity 5:
Physical Array: [60, 70, null, 30, 40, 50]
                  ↑   ↑         ↑
                rear  │       front
                     next

Iteration Order: 30 → 40 → 50 → 60 → 70
Physical Indices: 3 → 4 → 0 → 1 (wraps around)

Modular arithmetic: (3+1)%5=4, (4+1)%5=0, (0+1)%5=1, (1+1)%5=2
```

### Advanced Iteration Features

#### Iterator Protocol Implementation
```javascript
// Makes queue work with for...of loops
*[Symbol.iterator](){
  // Yield elements in FIFO order
}
```

#### Custom Iteration Methods
```javascript
// forEach similar to Array.forEach
forEach(callback){
  // Apply callback to each element
}

// entries() returns [position, value, physicalIndex]
*entries(){
  // Useful for debugging circular queues
}
```

## Time Complexity

| Operation | Simple Queue | Optimized Queue | Circular Queue |
|-----------|--------------|-----------------|----------------|
| Enqueue   | O(1)         | O(1)            | O(1)           |
| Dequeue   | O(n)         | O(1)            | O(1)           |
| Peek      | O(1)         | O(1)            | O(1)           |
| isEmpty   | O(1)         | O(1)            | O(1)           |
| Size      | O(1)         | O(1)            | O(1)           |
| **Iteration** | **O(n)**     | **O(n)**        | **O(n)**       |

**Space Complexity**: O(n) for all implementations

## Applications

### Real-world Applications:
1. **Operating Systems**: Process scheduling, handling requests
2. **Web Servers**: Managing incoming requests
3. **Printers**: Print job scheduling
4. **Breadth-First Search (BFS)**: Graph traversal algorithm
5. **Cache Implementation**: LRU (Least Recently Used) cache
6. **Call Centers**: Managing customer calls in order
7. **Keyboard Buffer**: Storing keystrokes

### Programming Applications:
- **Buffer for data streams**
- **Undo functionality** in applications
- **Asynchronous data transfer** (IO Buffers)
- **Simulation of real-world queues**

## Key Points to Remember

1. **FIFO Principle**: First element added is the first one removed
2. **Two main pointers**: Front (for dequeue) and Rear (for enqueue)
3. **Circular Queue advantage**: Efficient memory utilization
4. **Optimized Queue advantage**: O(1) dequeue operation
5. **Common mistake**: Writing `peak()` instead of `peek()`
6. **Iteration in Circular Queue**: Requires modular arithmetic to handle wraparound
7. **Iterator Protocol**: Enables `for...of` loops and spread operator usage

## Visual Summary

```
Simple Queue:    [Front] → [1][2][3][4] ← [Rear]
                           ↑           ↑
                        dequeue    enqueue
Iteration:       1 → 2 → 3 → 4

Optimized Queue: Front=2, Rear=5
                 {2: 20, 3: 30, 4: 40, 5: 50}
                  ↑                    ↑
                dequeue              enqueue
Iteration:       20 → 30 → 40 → 50

Circular Queue:  [1][2][3][4][5]
                  ↑           ↑
               front        rear
                (connects back when full)
Iteration:       Handle wraparound with (index + 1) % capacity
```

### Iteration Best Practices

1. **Use Iterator Protocol**: Implement `Symbol.iterator` for modern JS features
2. **Handle Empty Queues**: Always check if queue is empty before iteration
3. **Circular Queue Care**: Use modular arithmetic for proper wraparound
4. **Don't Modify During Iteration**: Avoid enqueue/dequeue operations while iterating
5. **Provide Multiple Iteration Methods**: `forEach`, `toArray`, `entries` for different use cases

This comprehensive guide now includes detailed explanations of iteration in all queue types, making it perfect for understanding both the theoretical concepts and practical implementation of queue data structures!