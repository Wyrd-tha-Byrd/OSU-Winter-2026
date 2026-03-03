- # #Graphs
	- A collection of objects in which pairs of objects are related or connected in some way
		- very generic description, basically everything can be represented as a graph
		- ### examples
			- Each node is an object or vertex in the network
			- maze
			- street maps
				- driving directions
			- Social media followers
			- Settlers of Catan (game board with information)
			- rhizomatic network
			- Linked lists
		- Talking about mathematical graph definition
			- ## Graph is represented as a set of:
				- $G=(V,E)$
				- $V=vertices$ (nodes, points)
				- $E=Edges$ (links, arcs) between pairs of vertices
					- Edges are representations of relationships between vertices
					- Two vertices are adjacent if there is a single edge between them 
					- Edges are represented as a pair $E={(V_1,V_2)}$
					- for each edge $e=(u,v) \exists E(G):$
						- can either be: 
							- undirected or 
								- bi-directional or arbitrary
							- directed from point to point
								- specific direction that affects order of traversal
					- ### Terminology
						- *Vertex* may have an edge to itself
						- The *Degree* of a vertex is the number of edges that are connected to it
							- ##### in-degree
								- input directional edges
							- ##### out-degree
								- output directional edges
							- determines time complexity of graph operations
						- Two nodes are *connected* if a path exists between them 
							- A-->B<--C
								- A and C are not connected 
						- #### Weighted Graphs
							- not all lengths are equal
							- used like road directions calculating the shortest path
							- *Weight* = Length or value of path
					- ### Operations:
						- Is X in graph?
						- Is Y reachable from X?
						- What nodes are reachable from X?
						- Are X and Y adjacent?
						- Whats the shortest path from X to Y?
						- How many edges are between A and Y?
						- Is there a Cycle in the Graph?
						- Can you start at node X visit all other nodes in the graph and return to X?
						- Is the graph connected?
					- ### Representations:
						- #### Adjacency list:
							- preferred for sparse graphs
							- unless otherwise specified this is assumed
							- stores a list a adjacent pairs to vertices and links them together into a graph
							- An array or hash table of |V| lists, on per vert
							- For each vert u in |V|:
								- ```python
								  adjacency_list[u] # contains all verts v such that there is an edge u,v in |E|
								  ```
							- ##### Space Required: $O(|V|+|E|)$
							- adding weights adds another layer to the edge data list
							- best for adding and deleting lots of nodes
						- #### Adjacency Matrix
							- Preferred for Dense Graphs
							- A 2D array og |V| rows and |V| columns 
							- For each vert u in V
							- ##### Space Required: $O(|V^2|)$
								```python
								 adjacency_matric[u][v]==1 #if there is an edge (u,v) in E
								```
							- adding a new node requires adding 1 to the size of all arrays as well as a new array
							- best for static graphs
						- 

| Adjacency Runtime Complexity | List                    | Matrix        |
| ---------------------------- | ----------------------- | ------------- |
| Space Complexity             | $\Theta(V+E)$           | $\Theta(V^2)$ |
| test if $(u,v) \exists E$    | $O(min(deg(u)))=O(V)$   | $O(1)$        |
| test if $u>v \exists E$      | $O(deg(u)) = O(V)$      | $O(1)$        |
| get out neighbors of $v$     | $\Theta(deg(u))-O(V)$   | $\Theta(V)$   |
| list all edges in $E$        | $\Theta(V+E)$           | $\Theta(V^2)$ |
| Insert Edge $(u,v)$          | $O(1)$                  | $O(1)$        |
| Delete edge $(u,v)$          | $O(deg(u)+deg(v))=O(V)$ | $O(1)$        |

- # Traversals
	- 