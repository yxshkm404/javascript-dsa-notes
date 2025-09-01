# Singly Linked List - Complete Guide

## What is a Linked List?

A **Linked List** is a linear data structure where elements are stored in nodes. Each node contains two parts:
- **Data**: The actual value stored in the node
- **Next**: A reference (pointer) to the next node in the sequence

Think of it like a chain where each link (node) is connected to the next one.

```
[Data|Next] -> [Data|Next] -> [Data|Next] -> null
```

## Why Use Linked Lists?

### Advantages:
- **Dynamic Size**: Can grow or shrink during runtime
- **Efficient Insertion/Deletion**: Easy to add/remove elements at the beginning
- **Memory Efficient**: Only uses memory for actual elements

### Disadvantages:
- **No Random Access**: Must traverse from the beginning to reach an element
- **Extra Memory**: Each node needs space for the pointer
- **Not Cache Friendly**: Nodes may be scattered in memory

## Basic Structure

### Node Class
```javascript
class Node {
  constructor(value) {
    this.value = value;  // Store the data
    this.next = null;    // Reference to next node
  }
}
```

### LinkedList Class
```javascript
class LinkedList {
  constructor() {
    this.head = null;  // First node in the list
    this.size = 0;     // Number of nodes
  }
}
```

## Core Operations

### 1. Check if Empty
Checks whether the list has any nodes.
```javascript
isEmpty() {
  return this.size === 0;
}
```

### 2. Get Size
Returns the number of nodes in the list.
```javascript
getSize() {
  return this.size;
}
```

### 3. Prepend (Add to Beginning)
Adds a new node at the start of the list.
```javascript
prepend(value) {
  const node = new Node(value);
  if (this.isEmpty()) {
    this.head = node;
  } else {
    node.next = this.head;  // New node points to current head
    this.head = node;       // New node becomes the head
  }
  this.size++;
}
```
**Visual Example:**
```
Before: [20] -> [30] -> null
After:  [10] -> [20] -> [30] -> null
```

### 4. Append (Add to End)
Adds a new node at the end of the list.
```javascript
append(value) {
  const node = new Node(value);
  if (this.isEmpty()) {
    this.head = node;
  } else {
    let curr = this.head;
    while (curr.next) {      // Traverse to the last node
      curr = curr.next;
    }
    curr.next = node;        // Link last node to new node
  }
  this.size++;
}
```
**Visual Example:**
```
Before: [10] -> [20] -> null
After:  [10] -> [20] -> [30] -> null
```

### 5. Insert at Index
Adds a node at a specific position.
```javascript
insert(value, index) {
  if (index < 0 || index > this.size) {
    return;  // Invalid index
  }
  if (index === 0) {
    this.prepend(value);  // Use existing method
  } else {
    const node = new Node(value);
    let prev = this.head;
    for (let i = 0; i < index - 1; i++) {
      prev = prev.next;   // Find node before insertion point
    }
    node.next = prev.next;  // New node points to next node
    prev.next = node;       // Previous node points to new node
    this.size++;
  }
}
```

### 6. Remove from Index
Removes a node at a specific position.
```javascript
removeFrom(index) {
  if (index < 0 || index >= this.size) {
    return null;
  }
  let removedNode;
  if (index === 0) {
    removedNode = this.head;
    this.head = this.head.next;
  } else {
    let prev = this.head;
    for (let i = 0; i < index - 1; i++) {
      prev = prev.next;
    }
    removedNode = prev.next;
    prev.next = removedNode.next;  // Skip the removed node
  }
  this.size--;
  return removedNode.value;
}
```

### 7. Remove by Value
Removes the first node with a specific value.
```javascript
removeValue(value) {
  if (this.isEmpty()) {
    return null;
  }
  if (this.head.value === value) {
    this.head = this.head.next;
    this.size--;
    return value;
  } else {
    let prev = this.head;
    while (prev.next && prev.next.value !== value) {
      prev = prev.next;
    }
    if (prev.next) {
      let removedNode = prev.next;
      prev.next = removedNode.next;
      this.size--;
      return value;
    }
    return null;
  }
}
```

### 8. Search
Finds the index of a value in the list.
```javascript
search(value) {
  if (this.isEmpty()) {
    return -1;
  }
  let i = 0;
  let curr = this.head;
  while (curr) {
    if (curr.value === value) {
      return i;  // Return index if found
    }
    curr = curr.next;
    i++;
  }
  return -1;  // Not found
}
```

### 9. Reverse
Reverses the order of nodes in the list.
```javascript
reverse() {
  let prev = null;
  let curr = this.head;
  while (curr) {
    let next = curr.next;  // Store next node
    curr.next = prev;      // Reverse the link
    prev = curr;           // Move prev forward
    curr = next;           // Move curr forward
  }
  this.head = prev;        // Update head
}
```
**Visual Example:**
```
Before: [10] -> [20] -> [30] -> null
After:  [30] -> [20] -> [10] -> null
```

### 10. Print
Displays all values in the list.
```javascript
print() {
  if (this.isEmpty()) {
    console.log("List is empty");
  } else {
    let curr = this.head;
    let list = "";
    while (curr) {
      list += `${curr.value}->`;
      curr = curr.next;
    }
    console.log(list);
  }
}
```

## Implementation Examples

### Basic Linked List Implementation
```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  isEmpty() {
    return this.size === 0;
  }

  getSize() {
    return this.size;
  }

  prepend(value) {
    const node = new Node(value);
    if (this.isEmpty()) {
      this.head = node;
    } else {
      node.next = this.head;
      this.head = node;
    }
    this.size++;
  }

  append(value) {
    const node = new Node(value);
    if (this.isEmpty()) {
      this.head = node;
    } else {
      let curr = this.head;
      while (curr.next) {
        curr = curr.next;
      }
      curr.next = node;
    }
    this.size++;
  }

  insert(value, index) {
    if (index < 0 || index > this.size) {
      return;
    }
    if (index === 0) {
      this.prepend(value);
    } else {
      const node = new Node(value);
      let prev = this.head;
      for (let i = 0; i < index - 1; i++) {
        prev = prev.next;
      }
      node.next = prev.next;
      prev.next = node;
      this.size++;
    }
  }

  removeFrom(index) {
    if (index < 0 || index >= this.size) {
      return null;
    }
    let removedNode;
    if (index === 0) {
      removedNode = this.head;
      this.head = this.head.next;
    } else {
      let prev = this.head;
      for (let i = 0; i < index - 1; i++) {
        prev = prev.next;
      }
      removedNode = prev.next;
      prev.next = removedNode.next;
    }
    this.size--;
    return removedNode.value;
  }

  removeValue(value) {
    if (this.isEmpty()) {
      return null;
    }
    if (this.head.value === value) {
      this.head = this.head.next;
      this.size--;
      return value;
    } else {
      let prev = this.head;
      while (prev.next && prev.next.value !== value) {
        prev = prev.next;
      }
      if (prev.next) {
        let removedNode = prev.next;
        prev.next = removedNode.next;
        this.size--;
        return value;
      }
      return null;
    }
  }

  search(value) {
    if (this.isEmpty()) {
      return -1;
    }
    let i = 0;
    let curr = this.head;
    while (curr) {
      if (curr.value === value) {
        return i;
      }
      curr = curr.next;
      i++;
    }
    return -1;
  }

  reverse() {
    let prev = null;
    let curr = this.head;
    while (curr) {
      let next = curr.next;
      curr.next = prev;
      prev = curr;
      curr = next;
    }
    this.head = prev;
  }

  print() {
    if (this.isEmpty()) {
      console.log("List is empty");
    } else {
      let curr = this.head;
      let list = "";
      while (curr) {
        list += `${curr.value}->`;
        curr = curr.next;
      }
      console.log(list);
    }
  }
}

// Example usage
const l = new LinkedList();
console.log(l.isEmpty());      // true
l.append(50);
l.prepend(20);
l.append(80);
l.insert(60, 2);
console.log(l.getSize());      // 4
l.print();                     // 20->50->60->80->
l.reverse();
l.print();                     // 80->60->50->20->
console.log(l.search(60));     // 1
l.removeFrom(3);
console.log(l.getSize());      // 3
l.print();                     // 80->60->50->
l.removeValue(60);
l.print();                     // 80->50->
console.log(l.getSize());      // 2
```

## Advanced Implementations

### 1. Linked List with Tail Pointer

Having a tail pointer makes append operations O(1) instead of O(n) because we don't need to traverse the entire list to find the last node.

**Visual Representation:**
```
Regular Linked List:
head → [10] → [20] → [30] → null
       ↑
    (only head pointer)

Linked List with Tail:
head → [10] → [20] → [30] → null
↑                      ↑
(head pointer)    (tail pointer)
```

**How Append Works with Tail:**
```
Step 1: Create new node [40]
Step 2: tail.next = newNode
Step 3: tail = newNode

Before:
head → [10] → [20] → [30] → null
                      ↑
                    tail

After:
head → [10] → [20] → [30] → [40] → null
                             ↑
                           tail
```

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  isEmpty() {
    return this.size === 0;
  }

  getSize() {
    return this.size;
  }

  prepend(value) {
    const node = new Node(value);
    if (this.isEmpty()) {
      this.head = node;
      this.tail = node;
    } else {
      node.next = this.head;
      this.head = node;
    }
    this.size++;
  }

  append(value) {
    const node = new Node(value);
    if (this.isEmpty()) {
      this.head = node;
      this.tail = node;
    } else {
      this.tail.next = node;
      this.tail = node;
    }
    this.size++;
  }

  removeFromFront() {
    if (this.isEmpty()) {
      return null;
    }
    const value = this.head.value;
    this.head = this.head.next;
    this.size--;
    return value;
  }

  removeFromEnd() {
    if (this.isEmpty()) {
      return null;
    }
    const value = this.tail.value;
    if (this.size === 1) {
      this.head = null;
      this.tail = null;
    } else {
      let prev = this.head;
      while (prev.next !== this.tail) {
        prev = prev.next;
      }
      prev.next = null;
      this.tail = prev;
    }
    this.size--;
    return value;
  }

  reverse() {
    let current = this.head;
    let prev = null;
    let next = null;
    while (current) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }
    this.tail = this.head;
    this.head = prev;
  }

  print() {
    if (this.isEmpty()) {
      console.log("List is empty");
    } else {
      let curr = this.head;
      let list = "";
      while (curr) {
        list += `${curr.value}->`;
        curr = curr.next;
      }
      console.log(list);
    }
  }
}

module.exports = LinkedList;
```

### 2. Stack Implementation using Linked List

A stack follows Last-In-First-Out (LIFO) principle. We use the head of the linked list as the top of the stack.

**Visual Representation:**
```
Push Operation:
Step 1: Push 10
Stack: [10] → null
       ↑
      top

Step 2: Push 20
Stack: [20] → [10] → null
       ↑
      top

Step 3: Push 30
Stack: [30] → [20] → [10] → null
       ↑
      top

Pop Operation:
Before: [30] → [20] → [10] → null
        ↑
       top

After:  [20] → [10] → null
        ↑
       top
(Returns 30)
```

**Stack Operations Mapping:**
- **Push** → Prepend to linked list (add at head)
- **Pop** → Remove from front (remove head)
- **Peek** → Return head value without removing

```javascript
const LinkedList = require("./linked-list-tail");

class LinkedListStack {
  constructor() {
    this.list = new LinkedList();
  }

  push(value) {
    this.list.prepend(value);
  }

  pop() {
    return this.list.removeFromFront();
  }

  peek() {
    return this.list.head.value;
  }

  isEmpty() {
    return this.list.isEmpty();
  }

  getSize() {
    return this.list.getSize();
  }

  print() {
    return this.list.print();
  }
}

// Example usage
const stack = new LinkedListStack();
console.log(stack.isEmpty());  // true
stack.push(20);
stack.push(10);
stack.push(30);
console.log(stack.getSize());  // 3
stack.print();                 // 30->10->20->
console.log(stack.pop());      // 30
stack.print();                 // 10->20->
console.log(stack.peek());     // 10
```

### 3. Queue Implementation using Linked List

A queue follows First-In-First-Out (FIFO) principle. We use the tail for enqueue and head for dequeue.

**Visual Representation:**
```
Enqueue Operation:
Step 1: Enqueue 10
Queue: [10] → null
       ↑      ↑
     front   rear

Step 2: Enqueue 20
Queue: [10] → [20] → null
       ↑       ↑
     front    rear

Step 3: Enqueue 30
Queue: [10] → [20] → [30] → null
       ↑              ↑
     front           rear

Dequeue Operation:
Before: [10] → [20] → [30] → null
        ↑              ↑
      front           rear

After:  [20] → [30] → null
        ↑       ↑
      front    rear
(Returns 10)
```

**Queue Operations Mapping:**
- **Enqueue** → Append to linked list (add at tail)
- **Dequeue** → Remove from front (remove head)
- **Peek** → Return head value without removing

```javascript
const LinkedList = require("./linked-list-tail");

class LinkedListQueue {
  constructor() {
    this.list = new LinkedList();
  }

  enqueue(value) {
    this.list.append(value);
  }

  dequeue() {
    return this.list.removeFromFront();
  }

  peek() {
    return this.list.head.value;
  }

  isEmpty() {
    return this.list.isEmpty();
  }

  getSize() {
    return this.list.getSize();
  }

  print() {
    return this.list.print();
  }
}

// Example usage
const queue = new LinkedListQueue();
console.log(queue.isEmpty());   // true
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);
console.log(queue.getSize());   // 3
queue.print();                  // 10->20->30->
console.log(queue.dequeue());   // 10
queue.print();                  // 20->30->
console.log(queue.peek());      // 20
```

**Why Use Linked List for Stack and Queue?**

1. **Dynamic Size**: No need to declare fixed size like arrays
2. **Efficient Operations**: O(1) for push/pop in stack and enqueue/dequeue in queue
3. **Memory Efficient**: Only uses memory for actual elements
4. **No Overflow**: Can grow as needed (limited only by system memory)

## Time Complexity

### Worst-Case Time Complexities (with tail implementation)

| Operation | Without Tail | With Tail | Worst Case Reason |
|-----------|-------------|-----------|-------------------|
| Prepend (insert at head) | O(1) | O(1) | Always just point new node to head. |
| Append (insert at tail) | O(n) | ✅ O(1) | Tail pointer avoids traversal to last node. |
| Insert at index | O(n) | O(n) | Still need traversal up to index - 1. |
| Remove at head | O(1) | O(1) | Just move head to head.next. |
| Remove at tail | O(n) | O(n) | Need traversal to find the previous node of tail (since singly linked). |
| Remove at index | O(n) | O(n) | Traversal required to reach that index. |
| Search by value | O(n) | O(n) | Still must check each node sequentially. |
| Reverse | O(n) | O(n) | Must visit all nodes and update pointers. |
| Print | O(n) | O(n) | Must traverse entire list. |

## Key Takeaways

1. **Use Linked Lists when:**
   - You need frequent insertion/deletion at the beginning
   - The size of data varies significantly
   - You don't need random access to elements

2. **Avoid Linked Lists when:**
   - You need to access elements by index frequently
   - Cache performance is critical
   - You need to minimize memory usage

3. **Remember:**
   - Always update the size when adding/removing nodes
   - Handle edge cases (empty list, single node)
   - Consider using a tail pointer for efficient append operations
