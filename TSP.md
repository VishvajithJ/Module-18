# Experiment 12(d): Travelling Salesman Problem (TSP)

## Aim
To write a Python program to find the shortest possible route that visits every city exactly once and returns to the starting point using the Travelling Salesman Problem (TSP) approach.

---

## Algorithm

1. **Input the Number of Cities**:
   - Begin by taking the number of cities as input.
   
2. **Distance Matrix**:
   - Define the distance matrix where each element `graph[i][j]` represents the distance between city `i` and city `j`.

3. **Generate All Permutations**:
   - Generate all possible permutations of the cities excluding the starting city.
   
4. **Calculate the Total Cost for Each Permutation**:
   - For each permutation, calculate the total distance of traveling through the cities in that order, starting and ending at the initial city.
   
5. **Track the Minimum Cost**:
   - Keep track of the minimum cost and the corresponding route.

6. **Return the Best Route and Minimum Cost**:
   - Once all permutations are evaluated, return the route with the minimum cost.

7. **End the Program**:
   - Output the minimum cost and the corresponding route.

---

## Program
```
from itertools import permutations

def tsp(graph, start=0):
    n = len(graph)
    vertices = list(range(n))
    vertices.remove(start)
    min_cost = float('inf')
    best_path = []

    for perm in permutations(vertices):
        cost = 0
        k = start
        for j in perm:
            cost += graph[k][j]
            k = j
        cost += graph[k][start]  # return to start

        if cost < min_cost:
            min_cost = cost
            best_path = [start] + list(perm) + [start]

    return min_cost, best_path

# Example graph (distance matrix)
graph = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

min_cost, path = tsp(graph)
print("Minimum cost:", min_cost)
print("Path:", path)

```

## OUTPUT

![image](https://github.com/user-attachments/assets/5072e4fb-3613-42b0-84cb-3aa3750c5cc8)


## RESULT
The program successfully finds the shortest possible route that visits all cities exactly once and returns to the starting city, along with the minimum travel cost.


