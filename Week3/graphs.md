# Graphs
Graphs are composed of nodes and edges and represent entities with directed or undirected connections to one another. Social connections, transport links, computer networks and biological processes are examples of common uses of graph data structures.

### directed graph
All the edges in a directed graph are uni-directional.  
Twitter follows only go in one direction.

### undirected graph
All the edges in an undirected graph are bi-directional or mutual.  
Facebook friendships are mutual.

### weighted graph
A weighted graph's edges have values assigned to them.

### unweighted graph
An unweighted graph's edges do not have values assigned to them.

### cyclic graph
A cyclic graph contains at least one graph cycle.

### acyclic graph
An acyclic graph does not contain any graph cycles.

### tree
A tree is a type of directed acyclic graph in which each node can only connect to nodes beneath it.
The DOM is a tree, as are family trees, taxonomies and filesystems.

### node
A node is an individual item in a graph.
A Facebook profile is a node.

### edge
An edge is a connection between two nodes. Edges can be uni-directional or bi-directional.
A Facebook friendship is an edge.

### first-degree connection
A first-degree connection exists between two nodes.
A - B - C : A has a first-degree connection with B.

### second-degree connection
A second-degree connection exists between nodes that do not connect to each other directly, but connect through another mutually-connected node.
A - B - C : A has a second-degree connection with C.

---

## Breadth First Search
Using an unweighted, acyclic, directed graph, such as a tree, filesystem etc.

```javascript
todo: [A, D, B, C];
shift 1st todo
find 1st todo connections
add numbers to todo
```