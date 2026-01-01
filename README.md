# DijkstraMesh

**DijkstraMesh** is a distributed graph-traversal engine built on the **Akka Typed** actor framework. It achieves high-concurrency pathfinding by mapping every vertex in a graph to a dedicated autonomous agent.

## 🧠 Architecture

Unlike traditional implementations, DijkstraMesh utilizes a **Multi-Agent System (MAS)**:

* **The Overseer:** Responsible for graph ingestion, vertex mapping, and routing user queries.
* **The Search Agents:** Each agent represents a unique source node. Upon initialization, agents compute the shortest path to all possible destinations in parallel.
* **The Protocol:** Uses a typed messaging system (`GraphSearchProtocol`) to ensure type-safe communication between the Overseer and the Mesh.

## 🛠 Features

* **Pre-computed Routing:** Shortest paths are calculated at startup, turning query requests into near-instant lookups.
* **Isolated State:** Each agent maintains its own graph clone, preventing shared-memory bottlenecks.
* **Weighted Edge Parsing:** Specifically designed to handle cost-based relationships between nodes.

## 📋 Input Format

The system parses a `Graph.txt` file using a bidirectional weight format.

**Current Graph Configuration:**

```text
Vertices: [A, B, C, D, E, F, G]
Edges: [A<-1->E, A<-2->C, B<-4->D, C<-1->D, D<-1->F, A<-3->F, F<-1->E, F<-2->G]

```

*Note: `A<-1->E` denotes a connection between A and E with a weight of 1.*

## 🚀 Getting Started

1. **Environment:** Ensure you have Java 11+ and the Akka Typed dependencies configured.
2. **File Setup:** Ensure your `Graph.txt` matches the format above and is placed in the project root.
3. **Launch:** Run the `main` method in `GraphSearchMultiAgentSystem`.
4. **Query:** Enter the Source and Destination nodes in the console to retrieve the pre-calculated path.
