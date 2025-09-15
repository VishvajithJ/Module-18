# Experiment 12(e): Count the Number of Triangles in an Undirected Graph

## AIM
To write a Python program to count the number of triangles present in an undirected graph.

---

## Algorithm

1. **Input the Graph**:
   - Start by taking the number of vertices as input.
   - Represent the graph using an adjacency matrix where `graph[i][j]` indicates the presence of an edge between vertices `i` and `j`.

2. **Matrix Multiplication**:
   - Initialize matrices `aux2` and `aux3` for storing the square and cube of the adjacency matrix respectively.
   - Multiply the adjacency matrix (`graph`) with itself to compute `aux2 = graph^2`.
   - Multiply the result (`aux2`) with the adjacency matrix again to compute `aux3 = graph^3`.

3. **Trace Calculation**:
   - The trace of a matrix is the sum of its diagonal elements. The diagonal elements of `aux3` represent the number of paths of length 3 starting and ending at each vertex.
   - Compute the trace of `aux3` to find the total number of triangles.

4. **Divide by 6**:
   - The number of triangles is the trace of `aux3` divided by 6. This is because each triangle is counted six times in the trace.

5. **Return the Result**:
   - The program outputs the number of triangles present in the undirected graph.

---

## Program
```
def multiply(A, B, C):
	global V
	for i in range(V):
		for j in range(V):
			C[i][j] = 0
			for k in range(V):
				C[i][j] += A[i][k] * B[k][j]

def getTrace(graph):
	global V
	trace = 0
	for i in range(V):
		trace += graph[i][i]
	return trace

def triangleInGraph(graph):
	global V
	
	# To Store graph^2
	aux2 = [[None] * V for i in range(V)]

	# To Store graph^3
	aux3 = [[None] * V for i in range(V)]

	for i in range(V):
		for j in range(V):
			aux2[i][j] = aux3[i][j] = 0

	# aux2 is graph^2 now printMatrix(aux2)
	multiply(graph, graph, aux2)
	multiply(graph, aux2, aux3)

	trace = getTrace(aux3)
	return trace // 6
V = int(input())
graph = [[0, 1, 1, 0],
		[1, 0, 1, 1],
		[1, 1, 0, 1],
		[0, 1, 1, 0]]

print("Total number of Triangle in Graph :",
					triangleInGraph(graph))



```

## OUTPUT
![image](https://github.com/user-attachments/assets/244cdd6d-525a-4678-bb3f-37b0cde9cc5c)


## RESULT

The program successfully counts the number of triangles in the given undirected graph by leveraging matrix multiplication and the trace property. The adjacency matrix is squared and cubed to find the number of 3-length cycles, and dividing the trace of the cubed matrix by 6 correctly accounts for repeated counts of each triangle. The output matches the expected number of triangles, verifying the correctness of the implementation.
