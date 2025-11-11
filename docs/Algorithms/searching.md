# 🔍 Searching Algorithms

## 📖 What is a Searching Algorithm?

A **searching algorithm** is a way to **find an item (element)** inside a collection of data (like an array or list).

> 💡 **Real-life example**: Finding a specific book in a library or looking for a contact in your phone!

---

## 🎯 Types of Searching Algorithms

### 1️⃣ Linear Search 📏
### 2️⃣ Binary Search ⚡

---

## 1️⃣ Linear Search 📏

### 🤔 **What is Linear Search?**
- Check each element **one by one** from start to end
- Like reading a book page by page to find a specific word
- **Easy to understand** but **slow for large data**

### ⏱️ **Time Complexity:** `O(n)` - Linear

### 🌟 **Real-life Example:**
Looking for a friend in your phone contact list by **scrolling from top to bottom** until you find them.

### 💻 **Code Implementation:**

```javascript
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;  // Found! Return the index
        }
    }
    return -1;  // Not found
}

// Test cases
console.log(linearSearch([-5, 2, 10, 4, 6], 10)); // Output: 2
console.log(linearSearch([-5, 2, 10, 4, 6], 6));  // Output: 4
console.log(linearSearch([-5, 2, 10, 4, 6], 20)); // Output: -1
```

---

## 🔍 Linear Search - Step by Step Examples

### 🎯 **Case 1:** `linearSearch([-5, 2, 10, 4, 6], 10)`
**Target = 10**

| Step | Index | Element | Match? | Action |
|------|-------|---------|--------|---------|
| 1 | 0 | -5 | ❌ | Continue |
| 2 | 1 | 2 | ❌ | Continue |
| 3 | 2 | 10 | ✅ | **Found!** Return `2` |

**Result:** `2` (index of element 10)

---

### 🎯 **Case 2:** `linearSearch([-5, 2, 10, 4, 6], 6)`
**Target = 6**

| Step | Index | Element | Match? | Action |
|------|-------|---------|--------|---------|
| 1 | 0 | -5 | ❌ | Continue |
| 2 | 1 | 2 | ❌ | Continue |
| 3 | 2 | 10 | ❌ | Continue |
| 4 | 3 | 4 | ❌ | Continue |
| 5 | 4 | 6 | ✅ | **Found!** Return `4` |

**Result:** `4` (index of element 6)

---

### 🎯 **Case 3:** `linearSearch([-5, 2, 10, 4, 6], 20)`
**Target = 20**

| Step | Index | Element | Match? | Action |
|------|-------|---------|--------|---------|
| 1 | 0 | -5 | ❌ | Continue |
| 2 | 1 | 2 | ❌ | Continue |
| 3 | 2 | 10 | ❌ | Continue |
| 4 | 3 | 4 | ❌ | Continue |
| 5 | 4 | 6 | ❌ | End of array |

**Result:** `-1` (element not found)

---

### 📝 **Linear Search Summary:**
- ✅ **Simple to understand and implement**
- ✅ **Works on both sorted and unsorted arrays**
- ❌ **Slow for large datasets**
- 🔄 **Checks every element from left to right**
- 📊 **Best Case:** O(1) - element found at first position
- 📊 **Worst Case:** O(n) - element at last position or not found

---

## 2️⃣ Binary Search ⚡

### 🤔 **What is Binary Search?**
- Works only on **sorted data**
- **Divide and conquer** approach
- Repeatedly divide the list into halves and check the middle
- **Much faster** than linear search

### ⏱️ **Time Complexity:** `O(log n)` - Logarithmic

### 🌟 **Real-life Example:**
Searching for a word in a **dictionary** by opening the middle page instead of starting from page 1. If the word you're looking for comes before the middle page, you search the left half; otherwise, you search the right half.

### ⚠️ **Important Condition:**
**Array must be sorted!** Binary search won't work on unsorted arrays.

### 💻 **Code Implementation:**

```javascript
function binarySearch(arr, target) {
    let leftIndex = 0;
    let rightIndex = arr.length - 1;
    
    while (leftIndex <= rightIndex) {
        let midIndex = Math.floor((leftIndex + rightIndex) / 2);
        
        if (target === arr[midIndex]) {
            return midIndex;  // Found!
        }
        
        if (target < arr[midIndex]) {
            rightIndex = midIndex - 1;  // Search left half
        } else {
            leftIndex = midIndex + 1;   // Search right half
        }
    }
    
    return -1;  // Not found
}

// Test cases (Note: array must be sorted!)
console.log(binarySearch([-5, 2, 4, 6, 10], 10)); // Output: 4
console.log(binarySearch([-5, 2, 4, 6, 10], 6));  // Output: 3
console.log(binarySearch([-5, 2, 4, 6, 10], 20)); // Output: -1
```

---

## 🔍 Binary Search - Step by Step Example

### 🎯 **Case:** `binarySearch([-5, 2, 4, 6, 10], 6)`
**Target = 6**

**Initial Setup:** `leftIndex = 0, rightIndex = 4`

| Step | Array Section | Left | Right | Mid | arr[mid] | Comparison | Next Action |
|------|---------------|------|-------|-----|----------|------------|-------------|
| 1 | `[-5,2,4,6,10]` | 0 | 4 | 2 | `4` | `6 > 4` | Search right half |
| 2 | `[6,10]` | 3 | 4 | 3 | `6` | `6 = 6` ✅ | **Found!** Return `3` |

### 🌳 **Visual Representation:**

```
Array: [-5, 2, 4, 6, 10]
        ↑           ↑
      left        right

Step 1: mid = 2, arr[2] = 4
        [-5, 2, 4, 6, 10]
                ↑
               mid
        4 < 6, so search right half

Step 2: mid = 3, arr[3] = 6  
        [-5, 2, 4, 6, 10]
                   ↑
                  mid
        6 = 6 ✅ FOUND at index 3!
```

---

## 📊 **Comparison: Linear vs Binary Search**

| Aspect | Linear Search 📏 | Binary Search ⚡ |
|--------|------------------|------------------|
| **Speed** | Slow `O(n)` | Fast `O(log n)` |
| **Data Requirement** | Any order | **Must be sorted** |
| **Implementation** | Simple | Moderate |
| **Memory** | O(1) | O(1) |
| **Best for** | Small/unsorted data | Large sorted data |

---

## 🎯 **When to Use Which?**

### 🔵 **Use Linear Search when:**
- Array is **small** (less than 100 elements)
- Array is **unsorted**
- You need to find **all occurrences** of an element
- **Simplicity** is more important than speed

### 🔴 **Use Binary Search when:**
- Array is **large** and **sorted**
- You need **maximum speed**
- Memory usage is not a concern
- Array doesn't change frequently

---

## 💡 **Quick Memory Tricks**

### 🧠 **Linear Search:**
> **"Line by Line"** - Check each element in a straight line

### 🧠 **Binary Search:**
> **"Divide to Decide"** - Cut the problem in half each time

---

## 🚀 **Key Takeaways**

✅ **Linear Search:**
- Simple but slow
- Works on any array
- Good for small datasets

✅ **Binary Search:**
- Fast but needs sorted data
- Perfect for large datasets
- Divide and conquer approach

---

## 🔗 **Practice Tips**

1. 🎯 **Start with Linear Search** - easier to understand
2. 📚 **Master Binary Search** - commonly asked in interviews  
3. 🧪 **Practice with different examples** - edge cases matter
4. ⏱️ **Understand time complexity** - crucial for interviews
5. 🔄 **Trace through examples manually** - builds intuition

---

💡 **Remember**: The right algorithm depends on your data and requirements. Choose wisely! 🎯