# Graph Data Structure in JavaScript

## What is a Graph?

A **Graph** is a data structure that consists of:
- **Vertices (Nodes)**: Individual points or elements
- **Edges**: Connections between vertices

Think of it like a social network where people are vertices and friendships are edges!

## Real-World Examples
- Social media connections (Facebook friends)
- City road networks
- Website page links
- Computer networks

## Graph Representation

Our implementation uses an **Adjacency List** - each vertex stores a list of its connected vertices.

```
Graph Structure:
{
  "A": Set{"B", "C"},
  "B": Set{"A", "C"},
  "C": Set{"A", "B"}
}
```

## Visual Representation

### Initial Empty Graph
```
adjacencyList = {}
```

### After Adding Vertices A, B, C
```
A: []
B: []
C: []
```

```
A     B     C
(isolated vertices - no connections)
```

### After Adding Edges A-B, A-C, B-C
```
A: [B, C]
B: [A, C] 
C: [A, B]
```

```
    A
   / \
  B---C

This forms a triangle where:
- A connects to B and C
- B connects to A and C  
- C connects to A and B
```

## Code Breakdown

### Constructor
```javascript
constructor() {
  this.adjacencyList = {};
}
```
**What it does**: Creates an empty object to store all vertices and their connections.

### addVertex(vertex)
```javascript
addVertex(vertex) {
  if (!this.adjacencyList[vertex]) {
    this.adjacencyList[vertex] = new Set();
  }
}
```

**What it does**: Adds a new vertex with no connections.

**Step by step**:
1. Check if vertex doesn't already exist
2. If new, create empty Set for this vertex
3. Set prevents duplicate connections

**Example**:
```javascript
graph.addVertex("A");
// Result: { "A": Set{} }
```

### addEdge(vertex1, vertex2)
```javascript
addEdge(vertex1, vertex2) {
  if (!this.adjacencyList[vertex1]) {
    this.addVertex(vertex1);
  }
  if (!this.adjacencyList[vertex2]) {
    this.addVertex(vertex2);
  }
  this.adjacencyList[vertex1].add(vertex2);
  this.adjacencyList[vertex2].add(vertex1);
}
```

**What it does**: Creates a connection between two vertices.

**Step by step**:
1. Check if vertex1 exists, if not create it
2. Check if vertex2 exists, if not create it
3. Add vertex2 to vertex1's connection list
4. Add vertex1 to vertex2's connection list (undirected graph)

**Visual Example**:
```javascript
graph.addEdge("A", "B");
```

Before:
```
A     B
```

After:
```
A-----B
```

### removeEdge(vertex1, vertex2)
```javascript
removeEdge(vertex1, vertex2) {
  this.adjacencyList[vertex1].delete(vertex2);
  this.adjacencyList[vertex2].delete(vertex1);
}
```

**What it does**: Removes the connection between two vertices.

**Step by step**:
1. Remove vertex2 from vertex1's connections
2. Remove vertex1 from vertex2's connections

### removeVertex(vertex)
```javascript
removeVertex(vertex) {
  if (!this.adjacencyList[vertex]) {
    return;
  }
  for (let adjacentVertex of this.adjacencyList[vertex]) {
    this.removeEdge(vertex, adjacentVertex);
  }
  delete this.adjacencyList[vertex];
}
```

**What it does**: Completely removes a vertex and all its connections.

**Step by step**:
1. Check if vertex exists
2. Remove all edges connected to this vertex
3. Delete the vertex from the adjacency list

### hasEdge(vertex1, vertex2)
```javascript
hasEdge(vertex1, vertex2) {
  return (
    this.adjacencyList[vertex1].has(vertex2) &&
    this.adjacencyList[vertex2].has(vertex1)
  );
}
```

**What it does**: Checks if two vertices are connected.

**Returns**: `true` if connected, `false` if not.

### display()
```javascript
display() {
  for (let vertex in this.adjacencyList) {
    console.log(vertex + " -> " + [...this.adjacencyList[vertex]]);
  }
}
```

**What it does**: Shows all vertices and their connections.

## Step-by-Step Execution of Your Code

### Step 1: Create Graph and Add Vertices
```javascript
const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
```

**Result**:
```
A: []
B: []
C: []
```

**Visual**:
```
A     B     C
```

### Step 2: Add Edges
```javascript
graph.addEdge("A", "B");
graph.addEdge("A", "C");
graph.addEdge("B", "C");
```

**Result**:
```
A: [B, C]
B: [A, C]
C: [A, B]
```

**Visual**:
```
    A
   / \
  B---C
```

### Step 3: Display Graph
```javascript
graph.display();
```

**Output**:
```
A -> B,C
B -> A,C
C -> A,B
```

### Step 4: Remove Edge A-B
```javascript
graph.removeEdge("A", "B");
graph.display();
```

**Result**:
```
A: [C]
B: [C]
C: [A, B]
```

**Visual**:
```
A   B
 \ /
  C
```

**Output**:
```
A -> C
B -> C
C -> A,B
```

### Step 5: Remove Vertex A
```javascript
graph.removeVertex("A");
graph.display();
```

**Result**:
```
B: [C]
C: [B]
```

**Visual**:
```
B---C
```

**Output**:
```
B -> C
C -> B
```

## Key Points for Beginners

1. **Undirected Graph**: When you add an edge A-B, it automatically creates B-A
2. **Set Usage**: Prevents duplicate connections
3. **Adjacency List**: Each vertex stores its neighbors
4. **Memory Efficient**: Only stores existing connections

## Common Use Cases

- **Social Networks**: Friend connections
- **Maps**: City connections via roads
- **Web Pages**: Link structures
- **Networks**: Computer connections

## Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| Add Vertex | O(1) |
| Add Edge | O(1) |
| Remove Edge | O(1) |
| Remove Vertex | O(degree) |
| Check Edge | O(1) |

## Practice Exercises

1. Try adding more vertices (D, E, F)
2. Create different connection patterns
3. Implement a method to count total edges
4. Add a method to find all neighbors of a vertex

This graph implementation is perfect for understanding basic graph concepts and building more complex graph algorithms!