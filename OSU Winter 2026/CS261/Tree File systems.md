# Computer File system
# Root main
- Every child folder has a parent that has a parent and so forth
# Can Be Used In:
Non-/Binary Decision Trees
# Properties
- Non-linear data structure
- represents data as a hierarchical struct
- Relationships between elements in the tree is encoded into the struct of the tree
	- Main -> Folder1 -> Folder1a -> FileA
# Terminology
- ## Node: 
	- each individual data element in a tree 
	- contains data element and pointers to other nodes
	- ### Root:
		- Ancestor of all other nodes of the tree
			- each tree has only one root
	- ### Interior Node:
		- A node with at least one child
	- ### Leaf Node:
		- A node that has no children
		- 
- ## Edge: 
- A parent/child relationship between data elements.
- represents directed relationships
	- ### Parent: 
		- a node that has pointers to other nodes
	- ### Child: 
		- a node that has a parent node
	- ### Sibling: 
		- two nodes are siblings if they both share the same parent node
	- ### Descendant: 
		- The descendants of the node N are any node that can be reached from N
	- ### Ancestor: 
		- An ancestor of node N is any node that has N as a descendant
- ## Paths:
	- ### Path:
		- The sequence of node to reach a descendant 
	- ### Height:
		- the number of edges between the root and any other node
			- the root has height 0
- ## Trees are recursive
	- ### Tree invariant:
		- Each node in the structure may have only one parent
		- the edges of the structure must not cycle
		- the edges of the struct cannot connect a node to itself
		- edges must be directed
	- ### Binary Trees
		- Binary Tree:
			- Full:
				- A binary tree that is full has all possible spots filled to the maximum # of Nodes
			- Perfect: 
				- Where all the leaves are the same level
				- Height: 
					- tree with n nodes is log(n)
					- it has 2^h leaves
					- it
			- Search Tree:
				- Ordered left and right matter
				- Search Operation:
					-  Input: sorted order, array
					- takes log(n) time to find 
					- Process:
						- divide input space in half
						- Look for half with close data
							- input space //2
							- is search for # greater or lesser than index(input // 2)
					- Output:
						- Searched number is there = true
						- searched numbeer is absent = false
				- Operations:
					- Insert(x) - 
						- searches for ordered parent to insert value as a child of
					- Search(x) -
						- Searches for a value
					- Remove(x) - 
						- Searches for the value
						- removes value from array
						- Cases to consider:
							- Remove a node with no children (leaf)
								- Best Case
									- Just remove the leaf
									- no structural effect
							- Remove a node with only one child
								- Easy Case
									- Remove node
									- update child relationship to replace parent
							- remove a child two children
								- Hard Case
								- multistep process
									- 
					- Find(x) -
						- Tree operations always start at root
						- Compare the current values against the search value
							- If root is none, return None
							- If it matches, return current node
							- If it doesn't
								- recursive compare current node against search value
									- x < s
										- left path
									- x > s
										- right path
		- Arbitrarily divides by left and right			
			- Left Subtree:
				- Left Child:
				
			- Right Subtree:
				- Right Child
```python
  class TreeNode:

	   left: 'TreeNode | None'

	   right: 'TreeNode | None'

	    data: int

  

    def __init__(self, data: int) -> None:

        self.left = None

        self.right = None

        self.data = data

  

    def __str__(self) -> str:

        return str(self.data)

  

    def print_tree(self, depth: int = 0) -> None:

        """helper method prints out the tree oriented horizontally, a 90 degree

        rotation from the usual top-down view."""

        if self.right:

            self.right.print_tree(depth + 1)

        print("    " * depth, self.data)

        if self.left:

            self.left.print_tree(depth + 1)

  
  

class BinarySearchTree:

    root: TreeNode | None

  

    def __init__(self) -> None:

        self.root = None

    def get_root(self) -> TreeNode | None:

        return self.root

			  ```
			  