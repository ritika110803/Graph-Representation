C Program: Graph Representation Using Adjacency List

This project demonstrates how to represent an *undirected graph* using an *Adjacency List* in C.

---

Description

This program:

* Uses a structure (struct Node) to represent graph nodes
* Implements an adjacency list using an array of linked lists
* Adds edges to the graph
* Displays the graph structure

The graph is implemented as *undirected*, meaning each edge connects two vertices in both directions.

---

What is an Adjacency List?

An *adjacency list* represents a graph as:

* An array of linked lists
* Each index represents a vertex
* Each linked list stores all adjacent vertices

This method is memory efficient compared to an adjacency matrix for sparse graphs.

---

Example Graph

The program creates a graph with:

* *4 vertices (0, 1, 2, 3)*
* *4 edges*

Edges added:

* (0 — 1)
* (0 — 2)
* (1 — 2)
* (2 — 3)

---

Graph Visualization

![Image](https://www.log2base2.com/images/ds/undirected-graph.png)

![Image](https://www.researchgate.net/profile/Stein-Malerud/publication/252675933/figure/fig1/AS%3A652972975476737%401532692297739/A-simple-undirected-graph-with-nodes-and-edges_Q320.jpg)

---

Source Code

c

#include <stdio.h>

#include <stdlib.h>

#define MAX 100

struct Node {
  
    int vertex;
    struct Node* next;
};

struct Node* adjList[MAX];

struct Node* createNode(int v) {
   
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
   
    newNode->vertex = v;
    newNode->next = NULL;
    return newNode;
}

void addEdge(int u, int v) {
    
    struct Node* newNode = createNode(v);
    
    newNode->next = adjList[u];
    adjList[u] = newNode;

    newNode = createNode(u);
    newNode->next = adjList[v];
    adjList[v] = newNode;
}

void displayGraph(int vertices) {
    
    int i;
    for(i = 0; i < vertices; i++) {
        
        struct Node* temp = adjList[i];
        
        printf("%d -> ", i);
        while(temp != NULL) {
            printf("%d -> ", temp->vertex);
            temp = temp->next;
        }
        printf("NULL\n");
    }
}

int main() {
    
    int vertices = 4;

    for(int i = 0; i < MAX; i++)
        adjList[i] = NULL;

    addEdge(0,1);
    addEdge(0,2);
    addEdge(1,2);
    addEdge(2,3);

    printf("Graph Representation:\n");
    displayGraph(vertices);

    return 0;
}


---

How to Compile and Run

Using GCC

1. Save the file as graph_adj_list.c
2. Open terminal / command prompt
3. Compile:

bash
gcc graph_adj_list.c -o graph


4. Run:

bash
./graph


(On Windows: graph.exe)

---

Sample Output


Graph Representation:
0 -> 2 -> 1 -> NULL
1 -> 2 -> 0 -> NULL
2 -> 3 -> 1 -> 0 -> NULL
3 -> 2 -> NULL


(Note: Order may vary because nodes are inserted at the beginning of the list.)

---

Time and Space Complexity

| Operation     | Complexity |
| ------------- | ---------- |
| Add Edge      | O(1)       |
| Display Graph | O(V + E)   |
| Space Used    | O(V + E)   |

Where:

* *V* = number of vertices
* *E* = number of edges

---

Concepts Covered

* Graph Data Structure
* Adjacency List Representation
* Linked Lists
* Dynamic Memory Allocation
* Undirected Graph Implementation

---

Possible Improvements

* Add user input for vertices and edges
* Implement DFS (Depth First Search)
* Implement BFS (Breadth First Search)
* Convert to directed graph
* Free allocated memory
* Use dynamic vertex count instead of fixed MAX

---
