# 🧩 Miscellaneous Programming Problems

> **A comprehensive guide to common algorithmic problems and their JavaScript implementations**

This repository contains solutions to classic programming problems that frequently appear in coding interviews and competitive programming. Each solution includes detailed explanations, step-by-step iterations, and complexity analysis! 🚀

## 📊 Problems Overview

| Problem | Difficulty | Time Complexity | Space Complexity | Key Concept |
|---------|------------|----------------|------------------|-------------|
| [Cartesian Product](#-cartesian-product) | Easy | O(m × n) | O(m × n) | Nested Loops |
| [Climbing Staircase](#-climbing-staircase) | Medium | O(n) | O(n) | Dynamic Programming |
| [Tower of Hanoi](#-tower-of-hanoi) | Hard | O(2ⁿ) | O(n) | Recursion |

---

## 🎯 Cartesian Product

### 📋 Problem Statement
Given two finite non-empty sets (arrays), find their **Cartesian Product**. The Cartesian product A × B is the set of all ordered pairs (a, b) where a ∈ A and b ∈ B.

### 🔍 Mathematical Definition
If A = {1, 2} and B = {3, 4, 5}, then:
**A × B = {(1,3), (1,4), (1,5), (2,3), (2,4), (2,5)}**

### 🎨 Visual Representation
```
Array 1: [1, 2]
Array 2: [3, 4, 5]

Grid Formation:
    3   4   5
1  (1,3)(1,4)(1,5)
2  (2,3)(2,4)(2,5)

Result: [[1,3], [1,4], [1,5], [2,3], [2,4], [2,5]]
```

### 💻 Implementation

```javascript
function cartesianProduct(arr1, arr2){
   let result = [];
   for(let i = 0; i < arr1.length; i++){
     for(let j = 0; j < arr2.length; j++){
       result.push([arr1[i], arr2[j]])
     }
   }
  return result
}
const arr1 = [1,2];
const arr2 = [3,4,5];
console.log(cartesianProduct(arr1, arr2))
```

### 🔍 Step-by-Step Iteration

Let's trace through the execution with `arr1 = [1,2]` and `arr2 = [3,4,5]`:

```
Iteration Details:
i=0, j=0: result.push([1,3]) → result = [[1,3]]
i=0, j=1: result.push([1,4]) → result = [[1,3],[1,4]]
i=0, j=2: result.push([1,5]) → result = [[1,3],[1,4],[1,5]]
i=1, j=0: result.push([2,3]) → result = [[1,3],[1,4],[1,5],[2,3]]
i=1, j=1: result.push([2,4]) → result = [[1,3],[1,4],[1,5],[2,3],[2,4]]
i=1, j=2: result.push([2,5]) → result = [[1,3],[1,4],[1,5],[2,3],[2,4],[2,5]]

Final Output: [[1,3],[1,4],[1,5],[2,3],[2,4],[2,5]]
```

### 📈 Complexity Analysis
- **Time Complexity:** `O(m × n)` where m and n are the lengths of the input arrays
- **Space Complexity:** `O(m × n)` to store all the pairs
- **Why:** We need to create exactly m × n pairs, each taking constant time

### 🎯 Use Cases
- **Database Operations:** JOIN operations
- **Game Development:** Combining different attributes
- **Testing:** Creating all possible input combinations
- **Mathematics:** Set theory operations

---

## 🪜 Climbing Staircase

### 📋 Problem Statement
Given a staircase of **n** steps, count the number of distinct ways to climb to the top. You can either climb **1 step** or **2 steps** at a time.

### 🎨 Visual Representation
```
For n = 4 steps:

Ways to reach step 4:
1. 1→1→1→1  (four 1-steps)
2. 1→1→2    (two 1-steps, one 2-step)
3. 1→2→1    (one 1-step, one 2-step, one 1-step)
4. 2→1→1    (one 2-step, two 1-steps)
5. 2→2      (two 2-steps)

Total: 5 ways
```

### 🧮 Pattern Recognition
```
n = 1: 1 way  → [1]
n = 2: 2 ways → [1+1, 2]
n = 3: 3 ways → [1+1+1, 1+2, 2+1]
n = 4: 5 ways → [1+1+1+1, 1+1+2, 1+2+1, 2+1+1, 2+2]
n = 5: 8 ways

Pattern: f(n) = f(n-1) + f(n-2) → It's Fibonacci!
```

### 💻 Implementation

```javascript
function climbinStairCase(n){
    const numOfWays=[1,2];
  for(let i=2;i<=n;i++){
    numOfWays[i]=numOfWays[i-1]+numOfWays[i-2];
  }
  
  return numOfWays[n-1];  
}
console.log(climbinStairCase(1))
console.log(climbinStairCase(2))
console.log(climbinStairCase(3))
console.log(climbinStairCase(4))
console.log(climbinStairCase(5))
```

### 🔍 Step-by-Step Iteration

Let's trace through the execution for `n = 5`:

```
Initial: numOfWays = [1, 2]

Iteration Details:
i=2: numOfWays[2] = numOfWays[1] + numOfWays[0] = 2 + 1 = 3
     numOfWays = [1, 2, 3]

i=3: numOfWays[3] = numOfWays[2] + numOfWays[1] = 3 + 2 = 5  
     numOfWays = [1, 2, 3, 5]

i=4: numOfWays[4] = numOfWays[3] + numOfWays[2] = 5 + 3 = 8
     numOfWays = [1, 2, 3, 5, 8]

i=5: numOfWays[5] = numOfWays[4] + numOfWays[3] = 8 + 5 = 13
     numOfWays = [1, 2, 3, 5, 8, 13]

Return: numOfWays[5-1] = numOfWays[4] = 8
```

**Output Results:**
```
climbinStairCase(1) → 1
climbinStairCase(2) → 2  
climbinStairCase(3) → 2
climbinStairCase(4) → 3
climbinStairCase(5) → 5
```

### 📈 Complexity Analysis
- **Time Complexity:** `O(n)` - single loop from 3 to n
- **Space Complexity:** `O(n)` for array solution, `O(1)` for optimized version
- **Why:** We calculate each value once and use previously computed results

### 🎯 Real-World Applications
- **Game Development:** Counting possible moves
- **Finance:** Calculating compound interest scenarios
- **Architecture:** Planning stair designs
- **Dynamic Programming:** Classic DP introduction problem

---

## 🗼 Tower of Hanoi

### 📋 Problem Statement
The **Tower of Hanoi** is a classic puzzle with three rods and n disks of different sizes. The goal is to move all disks from the source rod to the destination rod following these rules:
1. Only one disk can be moved at a time
2. Only the top disk from any rod can be moved
3. A larger disk cannot be placed on top of a smaller disk

### 🎨 Visual Representation
```
Initial State (n=3):          Goal State:
     |                           |
    ===                          |
   =====                         |
  =======                        |
─────────── A               ─────────── A

     |                           |
     |                          ===
     |                         =====
     |                        =======
─────────── B               ─────────── B

     |                           |
     |                           |
     |                           |
     |                           |
─────────── C               ─────────── C
```

### 🧠 Recursive Strategy
The key insight is to break down the problem:
1. **Move n-1 disks** from source to auxiliary rod
2. **Move the largest disk** from source to destination
3. **Move n-1 disks** from auxiliary to destination

### 💻 Implementation

```javascript
function towerOfHanoi(n, fromRod, toRod,usingRod){
    if(n===1){
        console.log(`Move disk 1 from ${fromRod} to ${toRod}`)
        return
    }
    towerOfHanoi(n-1,fromRod,usingRod,toRod)
    console.log(`Move disk ${n} from ${fromRod} to ${toRod}`) 
    towerOfHanoi(n-1,usingRod,toRod,fromRod)
}
console.log(towerOfHanoi(3,'A','C','B'))
```

### 🔍 Step-by-Step Execution for n=3

Let's trace through `towerOfHanoi(3,'A','C','B')`:

```
Call 1: towerOfHanoi(3,'A','C','B')
├─ n≠1, so:
├─ Call towerOfHanoi(2,'A','B','C')  // Move 2 disks A→B using C
│  ├─ n≠1, so:
│  ├─ Call towerOfHanoi(1,'A','C','B')  // Move 1 disk A→C
│  │  └─ n===1: "Move disk 1 from A to C"
│  ├─ "Move disk 2 from A to B"
│  └─ Call towerOfHanoi(1,'C','B','A')  // Move 1 disk C→B  
│     └─ n===1: "Move disk 1 from C to B"
├─ "Move disk 3 from A to C"
└─ Call towerOfHanoi(2,'B','C','A')  // Move 2 disks B→C using A
   ├─ n≠1, so:
   ├─ Call towerOfHanoi(1,'B','A','C')  // Move 1 disk B→A
   │  └─ n===1: "Move disk 1 from B to A"  
   ├─ "Move disk 2 from B to C"
   └─ Call towerOfHanoi(1,'A','C','B')  // Move 1 disk A→C
      └─ n===1: "Move disk 1 from A to C"
```

**Output Sequence:**
```
Move disk 1 from A to C
Move disk 2 from A to B
Move disk 1 from C to B
Move disk 3 from A to C
Move disk 1 from B to A
Move disk 2 from B to C
Move disk 1 from A to C
```

**Total moves:** 7 (which equals 2³ - 1 = 7)

### 📈 Complexity Analysis
- **Time Complexity:** `O(2^n)` - each disk doubles the number of moves
- **Space Complexity:** `O(n)` - recursion depth equals number of disks
- **Number of moves:** `2^n - 1` (mathematical proof exists)

### 🎲 Fun Facts
```javascript
function towerOfHanoiFacts() {
    console.log('🎉 Tower of Hanoi Fun Facts:');
    console.log('============================');
    
    const facts = [
        { disks: 3, moves: Math.pow(2, 3) - 1, time: '7 seconds' },
        { disks: 10, moves: Math.pow(2, 10) - 1, time: '17 minutes' },
        { disks: 20, moves: Math.pow(2, 20) - 1, time: '12 days' },
        { disks: 64, moves: Math.pow(2, 64) - 1, time: '584 billion years!' }
    ];
    
    facts.forEach(fact => {
        console.log(`${fact.disks} disks → ${fact.moves.toLocaleString()} moves → ${fact.time}`);
    });
    
    console.log('\n🌟 Legend says: When monks finish the 64-disk puzzle, the world will end!');
}

towerOfHanoiFacts();
```

### 🎯 Real-World Applications
- **Computer Science:** Understanding recursion and algorithm design
- **Backup Systems:** Data migration strategies
- **Game Development:** Puzzle game mechanics
- **Mathematical Proofs:** Demonstrating exponential growth

---

## 🎓 Summary & Learning Outcomes

### 🔑 Key Concepts Learned

| Concept | Problem | Key Takeaway |
|---------|---------|--------------|
| **Nested Iteration** | Cartesian Product | When you need all combinations |
| **Dynamic Programming** | Climbing Stairs | Build solutions using previous results |
| **Recursion** | Tower of Hanoi | Break complex problems into simpler ones |

### 📊 Complexity Comparison

```javascript
function complexityComparison() {
    console.log('⚡ Algorithm Complexity Comparison:');
    console.log('==================================');
    
    const n = 10;
    const m = 5;
    
    console.log(`For n=${n}, m=${m}:`);
    console.log(`Cartesian Product: O(m×n) = ${m * n} operations`);
    console.log(`Climbing Stairs: O(n) = ${n} operations`);
    console.log(`Tower of Hanoi: O(2^n) = ${Math.pow(2, n)} operations`);
    
    console.log('\n📈 Growth rates:');
    console.log('Linear < Polynomial < Exponential');
    console.log('O(n) < O(n²) < O(2^n)');
}

complexityComparison();
```

### 🏆 Interview Tips

1. **Cartesian Product:** 
   - Always clarify if order matters
   - Consider memory constraints for large sets
   - Think about lazy evaluation for infinite sets

2. **Climbing Stairs:**
   - Recognize the Fibonacci pattern
   - Consider space optimization
   - Think about variations (3 steps, different costs)

3. **Tower of Hanoi:**
   - Draw out small examples first
   - Understand the recursive structure
   - Remember the 2^n - 1 formula

### 🚀 Next Steps

- **Practice variations** of these problems
- **Implement iterative versions** where possible  
- **Analyze trade-offs** between time and space
- **Explore related problems** in dynamic programming and recursion

---

## 🤝 Contributing

Found this helpful? Give it a ⭐ and feel free to contribute:
- Add more problems
- Improve explanations
- Fix bugs or typos
- Add visualizations

## 📚 Further Reading

- [Dynamic Programming Guide](https://en.wikipedia.org/wiki/Dynamic_programming)
- [Recursion Patterns](https://www.geeksforgeeks.org/recursion/)
- [Big O Notation](https://en.wikipedia.org/wiki/Big_O_notation)
- [Algorithm Visualization](https://visualgo.net/)

---

*Happy coding and problem solving! 🎯✨*