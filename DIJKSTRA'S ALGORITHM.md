# Experiment 12(c): Dijkstra's Algorithm

## Aim
To write a Python program for Dijkstra's single-source shortest path algorithm.

---

## Algorithm

1. **Initialize Distance Array**:
   - Set the distance for all vertices to infinity (`∞`), except for the source vertex which is set to 0.

2. **Track Processed Vertices**:
   - Create a set `sptSet` to keep track of the processed vertices (shortest path tree).

3. **Pick the Minimum Distance Vertex**:
   - Select the vertex with the smallest distance that has not been processed.

4. **Update Adjacent Vertices**:
   - For the selected vertex, update the distances of its adjacent vertices if a shorter path is found through this vertex.

5. **Mark the Vertex as Processed**:
   - Once the vertex is processed, mark it as part of the shortest path tree.

6. **Repeat Steps**:
   - Continue the process until all vertices are processed.

7. **Print the Shortest Distances**:
   - Once all vertices are processed, print the shortest distances from the source vertex to all other vertices.

---

## Program

```
import sys

class Graph():

	def __init__(self, vertices):
		self.V = vertices
		self.graph = [[0 for column in range(vertices)]
					for row in range(vertices)]

	def printSolution(self, dist):
		print("Vertex   Distance from Source")
		for node in range(self.V):
			print(node, "           ", dist[node])

	def minDistance(self, dist, sptSet):

		min = sys.maxsize
		for u in range(self.V):
			if dist[u] < min and sptSet[u] == False:
				min = dist[u]
				min_index = u

		return min_index
	def dijkstra(self, src):

		dist = [sys.maxsize] * self.V
		dist[src] = 0
		sptSet = [False] * self.V

		for cout in range(self.V):
			x = self.minDistance(dist, sptSet)
			sptSet[x] = True
			for y in range(self.V):
				if self.graph[x][y] > 0 and sptSet[y] == False and 				dist[y] > dist[x] + self.graph[x][y]:
						dist[y] = dist[x] + self.graph[x][y]

		self.printSolution(dist)

# Driver program
g = Graph(9)
g.graph = [[0, 4, 0, 0, 0, 0, 0, 8, 0],
		[4, 0, 8, 0, 0, 0, 0, 11, 0],
		[0, 8, 0, 7, 0, 4, 0, 0, 2],
		[0, 0, 7, 0, 6, 14, 0, 0, 0],
		[0, 0, 0, 6, 0, 5, 0, 0, 0],
		[0, 0, 4, 14, 5, 0, 2, 0, 0],
		[0, 0, 0, 0, 0, 2, 0, 1, 6],
		[8, 11, 0, 0, 0, 0, 1, 0, 7],
		[0, 0, 2, 0, 0, 0, 6, 7, 0]
		];

g.dijkstra(0);




```

## OUTPUT
![image](https://github.com/user-attachments/assets/eca65761-0bd6-44f1-bd21-1c9b6944f8e8)

## RESULT

The program correctly implements Dijkstra's algorithm to find the shortest path from a source vertex to all other vertices in a weighted graph. It successfully initializes distances, iteratively selects the minimum distance vertex not yet processed, updates distances of adjacent vertices, and finally outputs the shortest distance from the source vertex to every other vertex. The output matches the expected shortest distances, confirming the algorithm's correctness and functionality.







