# HashMap in JavaScript

## What is a HashMap?

A HashMap (also known as Hash Table) is a data structure that implements an associative array abstract data type, a structure that can map keys to values. It uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

## Basic HashMap Implementation

```javascript
class HashMap {
    constructor(size = 16) {
        this.size = size;
        this.buckets = new Array(size);
        this.count = 0;
    }

    // Simple hash function
    hash(key) {
        let hash = 0;
        for (let i = 0; i < key.length; i++) {
            hash = (hash + key.charCodeAt(i) * i) % this.size;
        }
        return hash;
    }

    set(key, value) {
        const index = this.hash(key);
        
        if (!this.buckets[index]) {
            this.buckets[index] = [];
        }
        
        // Check if key already exists
        const existingItem = this.buckets[index].find(item => item[0] === key);
        if (existingItem) {
            existingItem[1] = value; // Update existing value
        } else {
            this.buckets[index].push([key, value]); // Add new key-value pair
            this.count++;
        }
    }

    get(key) {
        const index = this.hash(key);
        const bucket = this.buckets[index];
        
        if (bucket) {
            const item = bucket.find(item => item[0] === key);
            return item ? item[1] : undefined;
        }
        
        return undefined;
    }

    delete(key) {
        const index = this.hash(key);
        const bucket = this.buckets[index];
        
        if (bucket) {
            const itemIndex = bucket.findIndex(item => item[0] === key);
            if (itemIndex !== -1) {
                bucket.splice(itemIndex, 1);
                this.count--;
                return true;
            }
        }
        
        return false;
    }

    has(key) {
        return this.get(key) !== undefined;
    }

    keys() {
        const keys = [];
        for (const bucket of this.buckets) {
            if (bucket) {
                for (const [key] of bucket) {
                    keys.push(key);
                }
            }
        }
        return keys;
    }

    values() {
        const values = [];
        for (const bucket of this.buckets) {
            if (bucket) {
                for (const [, value] of bucket) {
                    values.push(value);
                }
            }
        }
        return values;
    }

    size() {
        return this.count;
    }
}
```

## Usage Example

```javascript
// Create a new HashMap
const hashMap = new HashMap(8);

// Add key-value pairs
hashMap.set("name", "John");
hashMap.set("age", 30);
hashMap.set("city", "New York");
hashMap.set("job", "Developer");

// Get values
console.log(hashMap.get("name")); // "John"
console.log(hashMap.get("age"));  // 30

// Check if key exists
console.log(hashMap.has("city")); // true
console.log(hashMap.has("country")); // false

// Get all keys and values
console.log(hashMap.keys());   // ["name", "age", "city", "job"]
console.log(hashMap.values()); // ["John", 30, "New York", "Developer"]

// Delete a key-value pair
hashMap.delete("age");
console.log(hashMap.get("age")); // undefined
```

## Hash Collisions

### What are Hash Collisions?

A hash collision occurs when two different keys produce the same hash value, meaning they would be stored in the same bucket of the hash table.

```
Visual representation of collision:

Hash Table (size = 8):
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  3  │  4  │  5  │  6  │  7  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

hash("apple") = 3
hash("grape") = 3  ← Collision! Both keys hash to index 3

After collision handling with chaining:
┌─────┬─────┬─────┬─────────────────────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  [apple:5][grape:8] │  4  │  5  │  6  │  7  │
└─────┴─────┴─────┴─────────────────────┴─────┴─────┴─────┴─────┘
                         Index 3
```

### Collision Resolution Methods

#### 1. Chaining (Used in our implementation above)

In chaining, each bucket contains a list (array) of key-value pairs. When a collision occurs, the new item is added to the list at that index.

```javascript
// Example of chaining collision handling
class HashMapWithChaining extends HashMap {
    displayStructure() {
        console.log("HashMap Structure:");
        for (let i = 0; i < this.size; i++) {
            if (this.buckets[i] && this.buckets[i].length > 0) {
                console.log(`Bucket ${i}:`, this.buckets[i]);
            } else {
                console.log(`Bucket ${i}: empty`);
            }
        }
    }
}

// Demonstrate collision
const hashMapChaining = new HashMapWithChaining(5);
hashMapChaining.set("ab", "value1");  // Might hash to index 2
hashMapChaining.set("ba", "value2");  // Might also hash to index 2 (collision)
hashMapChaining.displayStructure();
```

#### 2. Linear Probing (Open Addressing)

In linear probing, when a collision occurs, we look for the next available slot in the array.

```javascript
class HashMapLinearProbing {
    constructor(size = 16) {
        this.size = size;
        this.keys = new Array(size);
        this.values = new Array(size);
        this.count = 0;
    }

    hash(key) {
        let hash = 0;
        for (let i = 0; i < key.length; i++) {
            hash = (hash + key.charCodeAt(i) * i) % this.size;
        }
        return hash;
    }

    set(key, value) {
        if (this.count >= this.size * 0.7) {
            this.resize();
        }

        let index = this.hash(key);

        // Linear probing: find next available slot
        while (this.keys[index] !== undefined && this.keys[index] !== key) {
            index = (index + 1) % this.size;
        }

        // If it's a new key, increment count
        if (this.keys[index] === undefined) {
            this.count++;
        }

        this.keys[index] = key;
        this.values[index] = value;
    }

    get(key) {
        let index = this.hash(key);

        // Linear probing to find the key
        while (this.keys[index] !== undefined) {
            if (this.keys[index] === key) {
                return this.values[index];
            }
            index = (index + 1) % this.size;
        }

        return undefined;
    }

    resize() {
        const oldKeys = [...this.keys];
        const oldValues = [...this.values];

        this.size *= 2;
        this.keys = new Array(this.size);
        this.values = new Array(this.size);
        this.count = 0;

        // Rehash all existing keys
        for (let i = 0; i < oldKeys.length; i++) {
            if (oldKeys[i] !== undefined) {
                this.set(oldKeys[i], oldValues[i]);
            }
        }
    }
}
```

### Visual Representation of Linear Probing

```
Linear Probing Example:

Initial state:
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│     │     │     │     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
   0     1     2     3     4     5     6     7

Insert "apple" → hash("apple") = 3:
┌─────┬─────┬─────┬─────────┬─────┬─────┬─────┬─────┐
│     │     │     │ apple:5 │     │     │     │     │
└─────┴─────┴─────┴─────────┴─────┴─────┴─────┴─────┘
   0     1     2       3       4     5     6     7

Insert "grape" → hash("grape") = 3 (collision!):
Look for next empty slot: index 4
┌─────┬─────┬─────┬─────────┬─────────┬─────┬─────┬─────┐
│     │     │     │ apple:5 │ grape:8 │     │     │     │
└─────┴─────┴─────┴─────────┴─────────┴─────┴─────┴─────┘
   0     1     2       3         4       5     6     7
```

## Performance Comparison

| Operation | Average Case | Worst Case |
|-----------|-------------|------------|
| **Chaining** | | |
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |
| **Linear Probing** | | |
| Insert | O(1) | O(n) |
| Search | O(1) | O(n) |
| Delete | O(1) | O(n) |

## Load Factor and Resizing

The load factor is the ratio of the number of stored elements to the size of the hash table. A good load factor helps maintain performance:

```javascript
class DynamicHashMap extends HashMap {
    constructor(size = 16) {
        super(size);
        this.loadFactorThreshold = 0.75;
    }

    set(key, value) {
        super.set(key, value);
        
        // Check if resize is needed
        if (this.count / this.size > this.loadFactorThreshold) {
            this.resize();
        }
    }

    resize() {
        const oldBuckets = this.buckets;
        this.size *= 2;
        this.buckets = new Array(this.size);
        this.count = 0;

        // Rehash all existing key-value pairs
        for (const bucket of oldBuckets) {
            if (bucket) {
                for (const [key, value] of bucket) {
                    this.set(key, value);
                }
            }
        }
    }

    getLoadFactor() {
        return this.count / this.size;
    }
}
```

## Real-World Applications

1. **Database Indexing**: Fast lookups for database records
2. **Caching**: Store frequently accessed data for quick retrieval
3. **Symbol Tables**: In compilers and interpreters
4. **Associative Arrays**: Implementation of objects/dictionaries in programming languages
5. **Sets**: Implementing set data structures for unique elements

## Best Practices

1. **Choose a good hash function**: Minimizes collisions and distributes keys evenly
2. **Monitor load factor**: Keep it below 0.75 for optimal performance
3. **Handle collisions properly**: Choose between chaining and open addressing based on your use case
4. **Resize when necessary**: Maintain performance as the number of elements grows
5. **Consider memory usage**: Chaining uses more memory due to additional pointers

This implementation provides a solid foundation for understanding how HashMaps work in JavaScript, including collision handling strategies and performance considerations.
