# slippy1
1
Set A
A.Write a C program that accepts the vertices and edges of
a graph. Create adjacency list and display the adjacency list:
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
};
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*)
malloc(sizeof(struct Node));
newNode->vertex = v;
newNode->next = NULL;
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*)
malloc(sizeof(struct Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices *
sizeof(struct Node*));
int i;
for (i = 0; i < vertices; i++)
graph->adjLists[i] = NULL;
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
Assignment 4: Graph as adjacency list
2
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
}
void displayGraph(struct Graph* graph) {
int i;
for (i = 0; i < graph->numVertices; i++) {
struct Node* temp = graph->adjLists[i];
printf("\nAdjacency list of vertex %d:\n", i);
while (temp) {
printf("%d -> ", temp->vertex);
temp = temp->next;
}
printf("NULL\n");
}
}
int main() {
int vertices, edges, i, src, dest;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ",
i + 1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
displayGraph(graph);
3
return 0;
}
Output:-
Enter the number of vertices: 4
Enter the number of edges: 4
Enter edge 1 (source, destination): 1 2
Enter edge 2 (source, destination): 2 3
Enter edge 3 (source, destination): 3 4
Enter edge 4 (source, destination): 5 6
Adjacency list of vertex 0: NULL
Adjacency list of vertex 1:
2 -> NULL
Adjacency list of vertex 2:
3 -> 13449240 -> NULL
Adjacency list of vertex 3:
4 -> 2 -> NULL
B. Write a C program that accepts the vertices and edges of a
graph. Create adjacency list. Implement functions to print indegree,
outdegree and total degree of all vertex of graph.
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
int* inDegree;
int* outDegree;
};
4
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*)
malloc(sizeof(struct Node));
newNode->vertex = v;
newNode->next = NULL;
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*)
malloc(sizeof(struct Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices *
sizeof(struct Node*));
graph->inDegree = (int*) malloc(vertices *
sizeof(int));
graph->outDegree = (int*) malloc(vertices *
sizeof(int));
int i;
for (i = 0; i < vertices; i++) {
graph->adjLists[i] = NULL;
graph->inDegree[i] = 0;
graph->outDegree[i] = 0;
}
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
graph->outDegree[src]++;
graph->inDegree[dest]++;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
5
graph->outDegree[dest]++;
graph->inDegree[src]++;
}
void printDegrees(struct Graph* graph) {
int i;
for (i = 0; i < graph->numVertices; i++) {
printf("Vertex %d: in-degree = %d, out-degree =
%d, total degree = %d\n", i, graph->inDegree[i], graph-
>outDegree[i], graph->inDegree[i] + graph->outDegree[i]);
}
}
int main() {
int vertices, edges, i, src, dest;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ",
i + 1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
printDegrees(graph);
return 0;
}
Output: Enter the number of vertices: 5
Enter the number of edges: 4
6
Enter edge 1 (source, destination): 1 3
Enter edge 2 (source, destination): 2 3
Enter edge 3 (source, destination): 3 5
Enter edge 4 (source, destination): 6
7
Vertex 0: in-degree = 0, out-degree = 0, total degree = 0
Vertex 1: in-degree = 1, out-degree = 1, total degree = 2
Vertex 2: in-degree = 1, out-degree = 1, total degree = 2
Vertex 3: in-degree = 3, out-degree = 3, total degree = 6
Vertex 4: in-degree = 0, out-degree = 0, total degree = 0
Set B
A.Write a C program that accepts the vertices and edges of a graph and
store it as an adjacency list. Implement function to traverse the graph
using Breadth First Search (BFS) traversal.
#include <stdio.h>
#include <stdlib.h>
struct Node {
int vertex;
struct Node* next;
};
struct Graph {
int numVertices;
struct Node** adjLists;
int* visited;
};
struct Node* createNode(int v) {
struct Node* newNode = (struct Node*) malloc(sizeof(struct
Node));
newNode->vertex = v;
newNode->next = NULL;
7
return newNode;
}
struct Graph* createGraph(int vertices) {
struct Graph* graph = (struct Graph*) malloc(sizeof(struct
Graph));
graph->numVertices = vertices;
graph->adjLists = (struct Node**) malloc(vertices *
sizeof(struct Node*));
graph->visited = (int*) malloc(vertices * sizeof(int));
int i;
for (i = 0; i < vertices; i++) {
graph->adjLists[i] = NULL;
graph->visited[i] = 0;
}
return graph;
}
void addEdge(struct Graph* graph, int src, int dest) {
struct Node* newNode = createNode(dest);
newNode->next = graph->adjLists[src];
graph->adjLists[src] = newNode;
newNode = createNode(src);
newNode->next = graph->adjLists[dest];
graph->adjLists[dest] = newNode;
}
void BFS(struct Graph* graph, int startVertex) {
int queue[graph->numVertices];
int front = 0, rear = 0;
graph->visited[startVertex] = 1;
queue[rear] = startVertex;
rear++;
printf("BFS traversal starting from vertex %d: ",
startVertex);
while (front < rear) {
int currentVertex = queue[front];
printf("%d ", currentVertex);
8
front++;
struct Node* temp = graph->adjLists[currentVertex];
while (temp) {
int adjVertex = temp->vertex;
if (graph->visited[adjVertex] == 0) {
graph->visited[adjVertex] = 1;
queue[rear] = adjVertex;
rear++;
}
temp = temp->next;
}
}
}
int main() {
int vertices, edges, i, src, dest, startVertex;
printf("Enter the number of vertices: ");
scanf("%d", &vertices);
struct Graph* graph = createGraph(vertices);
printf("\nEnter the number of edges: ");
scanf("%d", &edges);
for (i = 0; i < edges; i++) {
printf("\nEnter edge %d (source, destination): ", i +
1);
scanf("%d%d", &src, &dest);
addEdge(graph, src, dest);
}
printf("\nEnter the starting vertex for BFS: ");
scanf("%d", &startVertex);
BFS(graph, startVertex);
return 0;
}
9
Output:- Enter the number of vertices: 5
Enter the number of edges: 6
Enter edge 1 (source, destination): 1 2
Enter edge 2 (source, destination): 2 3
Enter edge 3 (source, destination): 3 4
Enter edge 4 (source, destination): 4 5
Enter edge 5 (source, destination): 5 6
Enter edge 6 (source, destination): 3 7
Enter the starting vertex for BFS: 2
BFS traversal starting from vertex 2: 2 3 1 4
B. Write a C program that accepts the vertices and edges of a
graph and store it as an adjacency list. Implement function to
traverse the graph using Depth First Search (BFS) traversal.
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
typedef struct node {
int vertex;
struct node* next;
10
} node;
node* graph[MAX_VERTICES] = { NULL };
int visited[MAX_VERTICES] = { 0 };
void addEdge(int u, int v) {
node* newNode = (node*)malloc(sizeof(node));
newNode->vertex = v;
newNode->next = graph[u];
graph[u] = newNode;
}
void dfs(int vertex) {
visited[vertex] = 1;
printf("%d ", vertex);
node* ptr = graph[vertex];
while (ptr != NULL) {
int adjVertex = ptr->vertex;
if (!visited[adjVertex]) {
dfs(adjVertex);
}
ptr = ptr->next;
}
}
int main() {
int numVertices, numEdges;
printf("Enter the number of vertices: ");
scanf("%d", &numVertices);
printf("Enter the number of edges: ");
scanf("%d", &numEdges);
printf("Enter the edges (u, v):\n");
for (int i = 0; i < numEdges; i++) {
int u, v;
scanf("%d %d", &u, &v);
addEdge(u, v);
}
printf("Depth First Traversal: ");
for (int i = 0; i < numVertices; i++) {
11
if (!visited[i]) {
dfs(i);
}
}
return 0;
}
Output:
Enter the number of vertices: 4
Enter the number of edges: 3
Enter the edges (u, v):
1 2
2 4
4 6
Depth First Traversal: 0 1 2 4 6 3
Set c
B.Which data structure is used to implement Depth First Search?
Ans: Depth First Search (DFS) is typically implemented using a stack data structure. By
using a stack, DFS is able to explore all reachable nodes in a graph, visiting nodes in
depth-first order.
B. Where the new node is appended in Breadth-first search of OPEN
list?
Ans: In Breadth-first search (BFS), the new node is typically appended at the end of
the OPEN list.
C. What is complete graph?
12
Ans: . A complete graph is a type of graph in which every pair of distinct
vertices is connected by an edge. In other words, in a complete graph, every
vertex is directly connected to every other vertex.



Assignment 5
