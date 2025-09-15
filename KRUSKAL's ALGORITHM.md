# Experiment 12(b): Kruskal's Algorithm

## Aim
To write a Python program for Kruskal's algorithm to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph.

---

## Algorithm

1. **Sort all edges**:
   - Sort all the edges in non-decreasing order of their weights.

2. **Initialize parent and rank arrays**:
   - Initialize the `parent` array to keep track of the set to which each vertex belongs.
   - Initialize the `rank` array to manage the union of sets efficiently.

3. **Iterate over sorted edges**:
   - Pick the smallest edge and check if it forms a cycle with the MST formed so far by checking if the vertices are in the same set.
   
4. **Check and add the edge**:
   - If it doesn't form a cycle, include this edge in the MST and perform a union of the two sets.

5. **Repeat until MST contains V-1 edges**:
   - Continue adding edges to the MST until it contains `V-1` edges, where `V` is the number of vertices.

6. **Print the MST**:
   - Finally, print the edges in the MST along with the minimum cost.

---

## Program

```
from collections import defaultdict

class Graph:

	def __init__(self, vertices):
		self.V = vertices # No. of vertices
		self.graph = [] # default dictionary

	def addEdge(self, u, v, w):
		self.graph.append([u, v, w])

	def find(self, parent, i):
		if parent[i] == i:
			return i
		return self.find(parent, parent[i])

	def union(self, parent, rank, x, y):
		xroot = self.find(parent, x)
		yroot = self.find(parent, y)

		if rank[xroot] < rank[yroot]:
			parent[xroot] = yroot
		elif rank[xroot] > rank[yroot]:
			parent[yroot] = xroot
		else:
			parent[yroot] = xroot
			rank[xroot] += 1
	def KruskalMST(self):

		result = [] # This will store the resultant MST
		
		# An index variable, used for sorted edges
		i = 0
		
		# An index variable, used for result[]
		e = 0
		self.graph = sorted(self.graph,
							key=lambda item: item[2])

		parent = []
		rank = []

		for node in range(self.V):
			parent.append(node)
			rank.append(0)

		while e < self.V - 1:

			u, v, w = self.graph[i]
			i = i + 1
			x = self.find(parent, u)
			y = self.find(parent, v)

			if x != y:
				e = e + 1
				result.append([u, v, w])
				self.union(parent, rank, x, y)
			
		minimumCost = 0
		print ("Edges in the constructed MST")
		for u, v, weight in result:
			minimumCost += weight
			print("%d -- %d == %d" % (u, v, weight))
		print("Minimum Spanning Tree" , minimumCost)

g = Graph(4)
g.addEdge(0, 1, 10)
g.addEdge(0, 2, 6)
g.addEdge(0, 3, 5)
g.addEdge(1, 3, 15)
g.addEdge(2, 3, 4)

# Function call
g.KruskalMST()


```

## OUTPUT
![image](https://github.com/user-attachments/assets/fd0fd2bc-3dff-40a1-a2ba-5f504ac38d26)

## RESULT
The program correctly implemented Kruskal's algorithm for finding the Minimum Spanning Tree (MST) of a connected, undirected, weighted graph. It successfully sorted the edges by weight, efficiently detected cycles using the Union-Find data structure with path compression and union by rank, and included only edges that did not form cycles. The output displays the edges chosen for the MST along with their weights and the total minimum cost, confirming the algorithm's correct functionality.








