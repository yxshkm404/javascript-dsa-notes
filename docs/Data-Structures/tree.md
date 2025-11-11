# 🌳 Binary Search Tree (BST) Implementation

## Overview

A **Binary Search Tree (BST)** is a hierarchical data structure where each node has at most two children (left and right). The key property is that for any node:
- All values in the **left subtree** are **less than** the node's value
- All values in the **right subtree** are **greater than** the node's value

## Tree Structure

```
        10
       /  \
      5    15
     / \   / \
    3   7 13  17
   /
  2
```

## Implementation

### Node Class
```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
```

### BST Class
```javascript
class BinarySearchTree {
  constructor() {
    this.root = null;
  }
  
  isEmpty() {
    return this.root === null;
  }
}
```

## Operations

### 🔍 Search Operation
**Time Complexity:** O(log n) average, O(n) worst case

```javascript
search(root, value) {
  if (!root) return false;
  if (root.value === value) return true;
  
  return value < root.value 
    ? this.search(root.left, value)
    : this.search(root.right, value);
}
```

**Search Path Example:** Finding value `7`
```
    10 → 5 → 7 ✓
   /  \
  5    15
 / \
3   7
```

### ➕ Insert Operation
**Time Complexity:** O(log n) average, O(n) worst case

```javascript
insert(value) {
  const newNode = new Node(value);
  if (this.isEmpty()) {
    this.root = newNode;
  } else {
    this.insertNode(this.root, newNode);
  }
}

insertNode(root, newNode) {
  if (newNode.value < root.value) {
    if (root.left === null) {
      root.left = newNode;
    } else {
      this.insertNode(root.left, newNode);
    }
  } else {
    if (root.right === null) {
      root.right = newNode;
    } else {
      this.insertNode(root.right, newNode);
    }
  }
}
```

**Insert Process:** Adding value `4`
```
Before:          After:
   10               10
  /  \             /  \
 5    15          5    15
/ \              / \
3   7           3   7
               /
              4 (new)
```

### ❌ Delete Operation
**Time Complexity:** O(log n) average, O(n) worst case

Three cases to handle:
1. **Leaf node** (no children) → Simply remove
2. **One child** → Replace with child
3. **Two children** → Replace with inorder successor (smallest in right subtree)

```javascript
deleteNode(root, value) {
  if (root === null) return root;
  
  if (value < root.value) {
    root.left = this.deleteNode(root.left, value);
  } else if (value > root.value) {
    root.right = this.deleteNode(root.right, value);
  } else {
    // Node to delete found
    if (!root.left && !root.right) return null;        // Case 1
    if (!root.left) return root.right;                 // Case 2
    if (!root.right) return root.left;                 // Case 2
    
    // Case 3: Two children
    root.value = this.min(root.right);
    root.right = this.deleteNode(root.right, root.value);
  }
  return root;
}
```

### 🔢 Min/Max Operations
**Time Complexity:** O(log n) average, O(n) worst case

```javascript
min(root) {
  if (!root.left) return root.value;
  return this.min(root.left);
}

max(root) {
  if (!root.right) return root.value;
  return this.max(root.right);
}
```

## Traversal Methods

### 1. 📥 Inorder Traversal (Left → Root → Right)
**Result:** Sorted order of values
```
Traversal: 2, 3, 5, 7, 10, 13, 15, 17
```

### 2. 📤 Preorder Traversal (Root → Left → Right)
**Result:** Root appears first
```
Traversal: 10, 5, 3, 2, 7, 15, 13, 17
```

### 3. 📋 Postorder Traversal (Left → Right → Root)
**Result:** Root appears last
```
Traversal: 2, 3, 7, 5, 13, 17, 15, 10
```

### 4. 🌐 Level Order Traversal (Breadth-First)
**Result:** Level by level
```javascript
levelOrder() {
  const queue = [];
  queue.push(this.root);
  
  while (queue.length) {
    let curr = queue.shift();
    console.log(curr.value);
    
    if (curr.left) queue.push(curr.left);
    if (curr.right) queue.push(curr.right);
  }
}
```

**Visual representation:**
```
Level 1:     10
Level 2:    5  15
Level 3:   3 7 13 17
Level 4:  2
```

## Time & Space Complexity

| Operation | Average Case | Worst Case | Space |
|-----------|-------------|------------|-------|
| Search    | O(log n)    | O(n)       | O(1)  |
| Insert    | O(log n)    | O(n)       | O(1)  |
| Delete    | O(log n)    | O(n)       | O(1)  |
| Traversal | O(n)        | O(n)       | O(h)* |

*h = height of tree

## Usage Examples

```javascript
// Create a new BST
const bst = new BinarySearchTree();

// Insert values
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

// Search for values
console.log(bst.search(bst.root, 7));  // true
console.log(bst.search(bst.root, 20)); // false

// Get min/max values
console.log(bst.min(bst.root));        // 3
console.log(bst.max(bst.root));        // 15

// Tree height
console.log(bst.height(bst.root));     // 3

// Traversals
bst.inOrder(bst.root);    // 3, 5, 7, 10, 15
bst.levelOrder();         // 10, 5, 15, 3, 7
```

## 🎯 Key Benefits

- **Efficient Search:** O(log n) average case
- **Sorted Output:** Inorder traversal gives sorted sequence
- **Dynamic Size:** Can grow and shrink during runtime
- **No Extra Memory:** No need for sorted array maintenance

## ⚠️ Important Notes

- **Balanced vs Unbalanced:** Performance degrades to O(n) in worst case when tree becomes skewed
- **Self-Balancing Variants:** AVL trees and Red-Black trees maintain balance automatically
- **Duplicate Handling:** Current implementation places duplicates in right subtree

---

*This implementation provides a solid foundation for understanding Binary Search Trees and their core operations.*