#Introduction
A comprehensive summary of all changes made to ```A_Star_Search``` and ```maps.py```. Originally provided by The Coding Academy and later, Toi Ohomai Institute of Technology. All code changes were made by Nihal Dharmaraj.

This serves as documentation for an implementation of the A* Pathfinding algorithm originally authored by The Coding Academy. The original broken code can be seen in the _Original-Code_ branch.

The Algorithm searches through a 40x40 map, with 2 different sets of Starting and Goal positions (or nodes), with various obstacles in its path. 

Provided are _three_ basic heuristic models:
1. Euclidean Distance
2. Manhattan Distance (also known as Taxicab geometry)
3. Chebyshev Distance (also known as maximum metric)
These can be found at the beginning of the Algorithms section in the Jupyter notebook. 

## A_Star_Search.ipynb

### Imports
Added sys for querying size of objects.
```python
Import sys
```

### Algorithms
 Added Chebyshev distance, This is another popular heuristic distance model.
 ```
  d(x, y) = maxᵢ |xᵢ - yᵢ|
```
#### A* Search
Added PriorityQueue method call to initialize minheap for open_queue
```python
open_queue = PriorityQueue()
```

Added conditional printing flag and logic for F,G,H
```python
has_printed_data = False
# --/-- #
if has_printed_data is not True:
                    print(f"Values of f(N) = g(N) + h(N) at [{new_node.x},{new_node.y}]:\nf:{f:.3f}\ng:{g}\nh:(sqrt(({np.abs(goal_node.x - new_node.x)}^2) + ({np.abs(goal_node.y - new_node.y)}^2)) = {h:.3f})\n\n")
                    has_printed_data = True
```
Syntactically, this uses Chebyshev distance since that is the heuristic model the search algorithm uses in this implementation.

Added return values for break-out conditional for the main while loop.
```python
return path, len(discovered_nodes), cost_to_reach_goal_node, sys.getsizeof(discovered_nodes)
```
Later, added ```sys.getsizeof()``` function to benchmark BFS, DFS, and A* on an empty 800x800 (simulating large worst case O(t) and O(s)).

Updated g(N) calculation to use ```new_path``` instead of ```path```.
```python
g = 0
for i in range(len(new_path) - 1):
	g += distance(new_path[i], new_path[i+1])
```

### Search 1
Added dimensions (40x40) to ```map_height``` and ```map_width``` variables.
Added Start Node (0, 29) and Goal Node (39, 0) for _Agent_.
Populated print statements with relevant information and formatted appropriately.

### Search 2
Fixed typos in ```Search 2``` 
Added Start Node (0, 20) and Goal Node (39, 20) for _Agent_.
Populated print statements with relevant information and formatted appropriately.

## maps.py
Added 8 Obstacles to ```maps.py``` consisting of:
1. Circular Table at x:15, y:20 with a radius of 6
2. Rectangular Table at x:7, y:7 with (4 _w_ x 3 _h_)
3. Rectangular Table at x:25, y:12 with (6 _w_ x 2 _h_)
4. Rectangular Table at x:27, y:27 with (4 _w_ x 4 _h_)
5. Circular Table at x:7, y:27 with a radius of 2
6. Rectangular Table at x:33, y:4 with (3 _w_ x 4 _h_)
7. Rectangular Table at x:14, y:16 with (4 _w_ x 3 _h_)
8. Wall from x:[31-35], y:15

Fixed off-by 1 error in ```get_adjacent_nodes``` method and added check for if Node.x,y being ticked is value of 1 (wall) to print when _Agent_ encounters a wall while exploring.
```python
if not (i == 0 and j == 0):
	new_node = Node(node.x + i, node.y + j)
	if self._in_bounds_(new_node):
		if self.map[new_node.x, new_node.y] == 0:
			adjacent_nodes.append(new_node)
		elif self.map[new_node.x, new_node.y] == 1:
			print(f"Obstacle encoutered at: {new_node.x, new_node.y}")
```