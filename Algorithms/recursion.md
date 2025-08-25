# 🔄 Recursion

> **"To understand recursion, you must first understand recursion"** 😄

## 📖 What is Recursion?

**Recursion** is a problem-solving technique where the solution depends on solutions to smaller instances of the same problem.

### 🔑 Key Concepts:
- 🔁 **A function calls itself**
- 🎯 **Base case** - stops the recursion
- 📉 **Recursive case** - reduces the problem size
- 🚀 **Great technique to simplify complex solutions**

---

## 📊 Fibonacci Series

The Fibonacci sequence: `0, 1, 1, 2, 3, 5, 8, 13, 21...`

```javascript
function recursiveFibonacci(n) {
    // Base cases
    if (n < 2) {
        return n;
    }
    // Recursive case
    return recursiveFibonacci(n-1) + recursiveFibonacci(n-2);
}

console.log(recursiveFibonacci(8)); // Output: 21
```

### ⏱️ Time Complexity: `O(2^n)` - Exponential

---

## 🔢 Factorial

**Factorial** of n: `n! = n × (n-1) × (n-2) × ... × 1`

```javascript
function isFactorialRecursive(n) {
    // Base case
    if (n === 0) {
        return 1;
    }
    // Recursive case
    return n * isFactorialRecursive(n-1);
}

console.log(isFactorialRecursive(5)); // Output: 120
```

---

## 🧠 How Recursion Works - Step by Step

### 💭 Think of recursion like **a chain of tasks**:

👉 If you ask **"What is 5!?"**  
The function says: *"I don't know yet, but I know it is **5 × (something smaller)** → 4!"*

So it keeps asking itself with a smaller number **until it reaches the base case (0).**

---

## 🔍 Detailed Execution for `factorial(5)`

### 📥 **Call Stack (Going Down)**

| Step | Function Call | Question | Action |
|------|---------------|----------|---------|
| 1 | `factorial(5)` | Is `5 === 0`? ❌ | Return `5 × factorial(4)` |
| 2 | `factorial(4)` | Is `4 === 0`? ❌ | Return `4 × factorial(3)` |
| 3 | `factorial(3)` | Is `3 === 0`? ❌ | Return `3 × factorial(2)` |
| 4 | `factorial(2)` | Is `2 === 0`? ❌ | Return `2 × factorial(1)` |
| 5 | `factorial(1)` | Is `1 === 0`? ❌ | Return `1 × factorial(0)` |
| 6 | `factorial(0)` | Is `0 === 0`? ✅ | Return `1` 🛑 **BASE CASE** |

### 📤 **Unwinding (Coming Back Up)**

| Step | Calculation | Result |
|------|-------------|--------|
| 6 | `factorial(0)` | `= 1` |
| 5 | `factorial(1)` | `= 1 × 1 = 1` |
| 4 | `factorial(2)` | `= 2 × 1 = 2` |
| 3 | `factorial(3)` | `= 3 × 2 = 6` |
| 2 | `factorial(4)` | `= 4 × 6 = 24` |
| 1 | `factorial(5)` | `= 5 × 24 = 120` ✅ |

---

## 🎯 Recursion Cheat Sheet

### ✅ **Essential Components**

1. **🛑 Base Case** - When to stop
   ```javascript
   if (n === 0) return 1;  // Stop condition
   ```

2. **🔄 Recursive Case** - How to reduce the problem
   ```javascript
   return n * factorial(n-1);  // Smaller problem
   ```

### 💡 **Pro Tips**

| Tip | Description | Example |
|-----|-------------|---------|
| 🎯 **Always have a base case** | Prevents infinite recursion | `if (n <= 1) return n;` |
| 📉 **Make progress toward base case** | Each call should be "smaller" | `factorial(n-1)` not `factorial(n)` |
| 🧪 **Test with small inputs** | Easy to trace through | Start with `n=0, 1, 2` |
| ⚡ **Consider iterative alternatives** | Sometimes more efficient | Loops vs recursion |

### 🚨 **Common Pitfalls**

- ❌ **No base case** → Infinite recursion → Stack overflow
- ❌ **Wrong base case** → Incorrect results
- ❌ **Not making progress** → Infinite recursion

---

## 🎨 Visual Memory Aid

```
factorial(5)
    ├─ 5 × factorial(4)
           ├─ 4 × factorial(3)
                  ├─ 3 × factorial(2)
                         ├─ 2 × factorial(1)
                                ├─ 1 × factorial(0)
                                       └─ 1 ✅
                                ← 1 × 1 = 1
                         ← 2 × 1 = 2
                  ← 3 × 2 = 6
           ← 4 × 6 = 24
    ← 5 × 24 = 120 🎉
```

---

## 🔍 Recursive Binary Search

**Binary Search** efficiently finds a target element in a sorted array by repeatedly dividing the search space in half.

```javascript
function binarySearch(arr, target, left = 0, right = arr.length - 1) {
    // Base case: Target not found
    if (left > right) {
        return -1;
    }
    
    let mid = Math.floor((left + right) / 2);
    
    // Base case: Target found
    if (arr[mid] === target) {
        return mid;
    } 
    // Recursive case: Search left half
    else if (arr[mid] > target) {
        return binarySearch(arr, target, left, mid - 1);
    } 
    // Recursive case: Search right half
    else {
        return binarySearch(arr, target, mid + 1, right);
    }
}

// Example usage
let numbers = [1, 3, 5, 7, 9, 11];
let target = 7;
let result = binarySearch(numbers, target);

if (result !== -1) {
    console.log(`Element found at index: ${result}`); // Output: Element found at index: 3
} else {
    console.log("Element not found");
}
```

### ⏱️ Time Complexity: `O(log n)` - Logarithmic

---

## 🔍 Binary Search Execution - Step by Step

### 📊 **Searching for target = 7 in [1, 3, 5, 7, 9, 11]**

| Step | Array Range | Left | Right | Mid | arr[mid] | Comparison | Action |
|------|-------------|------|-------|-----|----------|------------|---------|
| 1 | `[1,3,5,7,9,11]` | 0 | 5 | 2 | `5` | `5 < 7` | Search right half |
| 2 | `[7,9,11]` | 3 | 5 | 4 | `9` | `9 > 7` | Search left half |
| 3 | `[7]` | 3 | 3 | 3 | `7` | `7 = 7` ✅ | **Found at index 3!** |

### 🌳 **Visual Call Stack**

```
binarySearch([1,3,5,7,9,11], 7, 0, 5)
    ├─ mid=2, arr[2]=5, 5<7 → search right
    └─ binarySearch([1,3,5,7,9,11], 7, 3, 5)
           ├─ mid=4, arr[4]=9, 9>7 → search left  
           └─ binarySearch([1,3,5,7,9,11], 7, 3, 3)
                  └─ mid=3, arr[3]=7, 7=7 → FOUND! Return 3 ✅
```

### 🧠 **How It Works:**
1. 🎯 **Divide**: Find the middle element
2. 🔍 **Compare**: Check if it's our target
3. ✂️ **Conquer**: Eliminate half of the remaining elements
4. 🔄 **Repeat**: Until found or no elements left

---

## 📚 Quick Reference

| Pattern | When to Use | Time Complexity | Space Complexity |
|---------|-------------|-----------------|------------------|
| **Fibonacci** | Overlapping subproblems | `O(2^n)` | `O(n)` |
| **Factorial** | Linear reduction | `O(n)` | `O(n)` |
| **Binary Search** | Sorted array search | `O(log n)` | `O(log n)` |

---

💡 **Remember**: Recursion is like peeling an onion - you keep removing layers until you reach the core (base case), then build back up! 🧅