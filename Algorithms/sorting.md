# 🔄 Sorting Algorithms in JavaScript

> **A comprehensive guide to understanding and implementing sorting algorithms in JavaScript**

Sorting algorithms are fundamental techniques used to arrange elements of an array in a particular order (usually ascending or descending). While JavaScript provides a built-in `Array.prototype.sort()` method, understanding these algorithms is crucial for writing efficient code and acing technical interviews! 🚀

## 📊 Algorithm Comparison Table

| Algorithm | Time Complexity | Space Complexity | Stability | Best Use Case |
|-----------|----------------|------------------|-----------|---------------|
| Bubble Sort | O(n²) | O(1) | Stable | Educational purposes |
| Selection Sort | O(n²) | O(1) | Unstable | Small datasets |
| Insertion Sort | O(n²) | O(1) | Stable | Nearly sorted data |
| Merge Sort | O(n log n) | O(n) | Stable | Large datasets |
| Quick Sort | O(n log n) | O(log n) | Unstable | General purpose |

---

## 1. 🫧 Bubble Sort

**How it works:** Repeatedly compares adjacent elements and swaps them if they're in the wrong order. Like bubbles rising to the surface!

### 🔍 Step-by-Step Visualization
```
Initial: [8, 20, -2, 4, -6]
Pass 1:  [8, -2, 4, -6, 20]  ← 20 bubbled to the end
Pass 2:  [-2, 4, -6, 8, 20]  ← 8 bubbled to position
Pass 3:  [-2, -6, 4, 8, 20]  ← 4 moved
Pass 4:  [-6, -2, 4, 8, 20]  ← Final sorted array
```

### 💻 Implementation

```javascript
function bubbleSort(arr) {
    let swapped;
    
    do {
        swapped = false; // Reset flag for each pass
        
        // Go through the array
        for (let i = 0; i < arr.length - 1; i++) {
            // Compare adjacent elements
            if (arr[i] > arr[i + 1]) {
                // Swap if they're in wrong order
                let temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;
                swapped = true; // Mark that we made a swap
            }
        }
    } while (swapped); // Continue until no swaps are made
    
    return arr;
}

// Example usage
console.log(bubbleSort([8, 20, -2, 4, -6]));
// Output: [-6, -2, 4, 8, 20]
```

**🎯 Key Points:**
- **Time Complexity:** O(n²) - worst and average case
- **Space Complexity:** O(1) - sorts in place
- **When to use:** Educational purposes (not recommended for real applications)

---

## 2. 🎯 Selection Sort

**How it works:** Finds the smallest element in the unsorted portion and places it at the beginning. Repeat until the entire array is sorted.

### 🔍 Step-by-Step Visualization
```
Initial: [8, 20, -2, 4, -6]
         
Step 1: Find minimum (-6), swap with first element
        [-6, 20, -2, 4, 8]
        [✓   unsorted portion  ]

Step 2: Find minimum (-2) in remaining, swap with second element
        [-6, -2, 20, 4, 8]
        [✓   ✓   unsorted   ]

Step 3: Find minimum (4) in remaining, swap with third element
        [-6, -2, 4, 20, 8]
        [✓   ✓  ✓  unsorted]

Step 4: Find minimum (8) in remaining, swap with fourth element
        [-6, -2, 4, 8, 20]
        [✓   ✓  ✓  ✓   ✓ ] ← All sorted!
```

### 💻 Implementation

```javascript
function selectionSort(arr) {
    const n = arr.length;
    
    // One by one move the boundary of unsorted subarray
    for (let i = 0; i < n - 1; i++) {
        // Find the minimum element in the remaining unsorted array
        let minIndex = i;
        
        // Check all elements after position i
        for (let j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j; // Update minimum index
            }
        }
        
        // Swap the found minimum element with the first element
        if (minIndex !== i) {
            let temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
        
        // Log progress for visualization
        console.log(`After iteration ${i + 1}:`, [...arr]);
    }
    
    return arr;
}

// Example with detailed output
console.log('Selection Sort Process:');
console.log('Initial array:', [8, 20, -2, 4, -6]);
console.log('Final result:', selectionSort([8, 20, -2, 4, -6]));

/* Output:
Selection Sort Process:
Initial array: [8, 20, -2, 4, -6]
After iteration 1: [-6, 20, -2, 4, 8]
After iteration 2: [-6, -2, 20, 4, 8]
After iteration 3: [-6, -2, 4, 20, 8]
After iteration 4: [-6, -2, 4, 8, 20]
Final result: [-6, -2, 4, 8, 20]
*/
```

**🎯 Key Points:**
- **Time Complexity:** O(n²) - always makes n² comparisons
- **Space Complexity:** O(1) - sorts in place
- **When to use:** When memory space is limited and you need predictable performance

---

## 3. 📝 Insertion Sort

**How it works:** Builds the sorted array one element at a time by inserting each element into its correct position among the previously sorted elements.

### 🔍 Step-by-Step Visualization
```
Initial: [8, 20, -2, 4, -6]

Step 1: [8] | [20, -2, 4, -6]  ← 8 is already "sorted"
Step 2: [8, 20] | [-2, 4, -6]  ← Insert 20 (already in place)
Step 3: [-2, 8, 20] | [4, -6]  ← Insert -2 at beginning
Step 4: [-2, 4, 8, 20] | [-6]  ← Insert 4 in correct position
Step 5: [-6, -2, 4, 8, 20] | [] ← Insert -6 at beginning
```

### 💻 Implementation

```javascript
function insertionSort(arr) {
    // Start from the second element (index 1)
    for (let i = 1; i < arr.length; i++) {
        let key = arr[i]; // Element to be inserted
        let j = i - 1;    // Last element of sorted portion
        
        console.log(`\nInserting ${key} into sorted portion: [${arr.slice(0, i)}]`);
        
        // Move elements greater than key one position ahead
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j]; // Shift element to the right
            j--;
        }
        
        // Insert the key at correct position
        arr[j + 1] = key;
        
        console.log(`After insertion: [${arr}]`);
    }
    
    return arr;
}

// Example with detailed output
console.log('Insertion Sort Process:');
console.log('Initial array:', [8, 20, -2, 4, -6]);
insertionSort([8, 20, -2, 4, -6]);

/* Output:
Insertion Sort Process:
Initial array: [8, 20, -2, 4, -6]

Inserting 20 into sorted portion: [8]
After insertion: [8,20,-2,4,-6]

Inserting -2 into sorted portion: [8,20]
After insertion: [-2,8,20,4,-6]

Inserting 4 into sorted portion: [-2,8,20]
After insertion: [-2,4,8,20,-6]

Inserting -6 into sorted portion: [-2,4,8,20]
After insertion: [-6,-2,4,8,20]
*/
```

**🎯 Key Points:**
- **Time Complexity:** O(n²) worst case, O(n) best case (already sorted)
- **Space Complexity:** O(1) - sorts in place
- **When to use:** Small datasets or nearly sorted data

---

## 4. 🔀 Merge Sort

**How it works:** Uses divide-and-conquer strategy - splits array into halves, sorts each half recursively, then merges them back together.

### 🔍 Divide and Conquer Visualization
```
                    [8, 20, -2, 4, -6]
                   /                   \
            [8, 20, -2]                [4, -6]
           /          \                /      \
      [8, 20]        [-2]         [4]      [-6]
      /    \          |            |         |
    [8]    [20]     [-2]         [4]      [-6]
     |      |        |            |         |
   Merge: [8, 20]  [-2]         [4]      [-6]
          \         /            \        /
         [-2, 8, 20]              [-6, 4]
                    \              /
                  [-6, -2, 4, 8, 20]
```

### 💻 Implementation

```javascript
function mergeSort(arr) {
    // Base case: array with 1 or 0 elements is already sorted
    if (arr.length < 2) {
        return arr;
    }
    
    // Divide: find the middle point
    const mid = Math.floor(arr.length / 2);
    const left = arr.slice(0, mid);   // Left half
    const right = arr.slice(mid);     // Right half
    
    console.log(`Dividing: [${arr}] → [${left}] | [${right}]`);
    
    // Conquer: recursively sort both halves and merge
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    const result = [];
    
    // Compare elements from both arrays and merge in sorted order
    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            result.push(left.shift()); // Take from left
        } else {
            result.push(right.shift()); // Take from right
        }
    }
    
    // Add any remaining elements
    const merged = [...result, ...left, ...right];
    console.log(`Merging: [${left.length ? left : 'empty'}] + [${right.length ? right : 'empty'}] → [${merged}]`);
    
    return merged;
}

// Example usage
console.log('Merge Sort Process:');
console.log('Final result:', mergeSort([8, 20, -2, 4, -6]));
```

**🎯 Key Points:**
- **Time Complexity:** O(n log n) - consistently efficient
- **Space Complexity:** O(n) - requires additional memory
- **When to use:** Large datasets where consistent performance is needed

---

## 5. ⚡ Quick Sort

**How it works:** Selects a 'pivot' element, partitions array into elements smaller and larger than pivot, then recursively sorts both partitions.

### 🔍 Partitioning Visualization
```
Initial: [8, 20, -2, 4, -6] (pivot = -6)

Partition: elements < -6 | pivot | elements > -6
          []              |  -6  |  [8, 20, -2, 4]

Recursively sort: [] + [-6] + quickSort([8, 20, -2, 4])
                              ↓
                        [8, 20, -2, 4] (pivot = 4)
                        [-2] | 4 | [8, 20]
                        ↓
                   [-2] + [4] + [8, 20]
                   
Final: [-6, -2, 4, 8, 20]
```

### 💻 Implementation

```javascript
function quickSort(arr) {
    // Base case: arrays with 0 or 1 element are already sorted
    if (arr.length <= 1) return arr;
    
    // Choose pivot (last element in this implementation)
    let pivot = arr[arr.length - 1];
    let left = [];   // Elements smaller than pivot
    let right = [];  // Elements larger than pivot
    
    console.log(`\nSorting: [${arr}] with pivot: ${pivot}`);
    
    // Partition: divide elements based on pivot
    for (let i = 0; i < arr.length - 1; i++) {
        if (arr[i] > pivot) {
            right.push(arr[i]);
        } else {
            left.push(arr[i]);
        }
    }
    
    console.log(`Partitioned: [${left}] | ${pivot} | [${right}]`);
    
    // Recursively sort left and right partitions, then combine
    return [...quickSort(left), pivot, ...quickSort(right)];
}

// Example usage
console.log('Quick Sort Process:');
console.log('Initial array:', [8, 20, -2, 4, -6]);
console.log('Final result:', quickSort([8, 20, -2, 4, -6]));

/* Output:
Quick Sort Process:
Initial array: [8, 20, -2, 4, -6]

Sorting: [8,20,-2,4,-6] with pivot: -6
Partitioned: [] | -6 | [8,20,-2,4]

Sorting: [8,20,-2,4] with pivot: 4
Partitioned: [-2] | 4 | [8,20]

Sorting: [8,20] with pivot: 20
Partitioned: [8] | 20 | []

Final result: [-6,-2,4,8,20]
*/
```

**🎯 Key Points:**
- **Time Complexity:** O(n log n) average, O(n²) worst case
- **Space Complexity:** O(log n) - due to recursion
- **When to use:** General-purpose sorting with good average performance

---

## 6. 🛠️ Built-in JavaScript `sort()`

JavaScript's built-in sort method is very convenient but has some quirks to be aware of:

### 💻 Basic Usage

```javascript
// ⚠️ Default behavior - sorts as strings!
let numbers = [10, 5, 100, 2, 1000];
console.log(numbers.sort()); 
// Output: [10, 100, 1000, 2, 5] ← Wrong for numbers!

// ✅ Correct way to sort numbers
console.log(numbers.sort((a, b) => a - b)); 
// Output: [2, 5, 10, 100, 1000] ← Correct!

// Sort in descending order
console.log(numbers.sort((a, b) => b - a)); 
// Output: [1000, 100, 10, 5, 2]

// Sort strings (default behavior works fine)
let fruits = ['banana', 'apple', 'cherry'];
console.log(fruits.sort()); 
// Output: ['apple', 'banana', 'cherry']
```

---

## 🎓 When to Use Each Algorithm

### 🚀 **For Learning & Interviews:**
- **Bubble Sort:** Understand the basics
- **Selection Sort:** Simple to implement and explain
- **Insertion Sort:** Good for small or nearly sorted data

### 🏭 **For Production Code:**
- **Merge Sort:** When you need guaranteed O(n log n) performance
- **Quick Sort:** General-purpose, usually fastest in practice
- **JavaScript's sort():** Most convenient for typical use cases

### 📊 **Performance Comparison**
```javascript
// Test function to compare algorithms
function compareAlgorithms() {
    const testArray = [64, 34, 25, 12, 22, 11, 90];
    
    console.log('Original:', testArray);
    console.log('Bubble Sort:', bubbleSort([...testArray]));
    console.log('Selection Sort:', selectionSort([...testArray]));
    console.log('Insertion Sort:', insertionSort([...testArray]));
    console.log('Merge Sort:', mergeSort([...testArray]));
    console.log('Quick Sort:', quickSort([...testArray]));
    console.log('Built-in Sort:', [...testArray].sort((a, b) => a - b));
}
```

## 🎯 Key Takeaways

1. **Understand the trade-offs:** Time vs Space complexity
2. **Choose the right tool:** Different algorithms for different scenarios
3. **Practice implementation:** Great for coding interviews
4. **Use built-in methods:** For most real-world applications
5. **Consider data characteristics:** Size, pre-sorted nature, memory constraints

---

## 🤝 Contributing

Found this helpful? Give it a ⭐ and feel free to contribute improvements or additional algorithms!

## 📚 Further Reading

- [Big O Notation Guide](https://en.wikipedia.org/wiki/Big_O_notation)
- [MDN Array.sort() Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [Visualization of Sorting Algorithms](https://visualgo.net/en/sorting)

---

*Happy coding! 🚀*