Another type of Tree structure
- priority queues
	- An ADT that associates a priority value with each element
		- dequeue() removes the element with the highest priority first
	- Used in:
		- Scheduling
		- Quotas/Traffic Management/Admission Control
		- Greedy Algorithms (I play pot of greed, which allows me to play 3 more algorithms from my hand)
		- Finding the top K elements of a dataset
	- The users view of a priority queue:
		- Head_20->18->14->12->10->6->4_tail
		- A priority queue is typically implemented using a data struct called a binary heap
- heaps
	- Complete binary tree in which every nodes value is greater or equal to the values of its children
		- this is called max heap
		- min heap: each nodes value is less than or equal to the value of its children
	- Recall: a complete binary tree is one that is filled except for the bottom level left to right
		- the longest path from root to leaf in such a tree is O(logn)
			- root36
		- 32                       10
	  24            16         7           8
    6         20  4        14  --------------
	- # Operations:
		- ### Insert(item) 
			- insert an item into the heap
			- always inserted at the very end of the leaves
				- and at the very first open spot
					- if the placement is wrong, solve:
						- percolate_up() to maintain the heap invariant 
							- (shift up, check, repeat until property is no longer violated)
							- parent node must be greater than children in max heap
								- or until root
			- the heap is always a complete binary tree
			- worst case is O(logn) time
		- ### remove(item) 
			- remove and return root from heap
			- removing the root needs to maintain heap invariants:
				- the heap must remain a complete binary tree
				- each nodes value must be greater than either of its children
			- Replace the root with the last element in the heap
				- end of array view or last on the right last level in tree view
				- swap the root with the last element in heap
					- Keep track of the head and last node in the heap
				- fix heap by percolating the new root node down percolate_down()
					- always perc down to the child with the highest value
					- while new value > child value
						- always end up with complete binary tree
						- last level must be populated left to right
			- worst case O(logn) time
			- edge cases:
				- Heap with only 1 element
				- Make sure the computed child index is not out of bounds
		- #### Peek(item) 
			- return max value without removing it
			- O(1) time
		- #### size() 
			- number of items in heap
			- O(1) time
		- # Implementation
			- Tree Ordering
				- #### Complete Binary Tree
					- Perform a level order numbering of nodes
						- 0 at root, 1 and 2 for its children and so on
							- root = index 0
							- left child of node $i = 2*i +1$
							- right child of node $i = 2*i +2$
							- parent = (i-1)//2
						- Array representation
							- ```python
									#			36
									#	    32 /  \ 10
									#	 24/ \16,  7/ \8
									#	6/\20,4/\14.-----
							  
							  array = [36,32,10,24,16,7,8,6,20,4,14]
							  ```
				- #### Array Efficiency
					- Usually only for complete binary trees
					- Missing nodes become null entries in the array
							- could waste a lot of space when big gaps occur
				- #### Building a Heap
					- given an array in arb order how do we build?
						- simple answer: create a heap and insert each element
							- runtime complexity: O(nlogn)
							- Space Complexity: O(n)
								- linear because we start at 0 element heap and end with an n element heap
					- Heapify - Faster
						- Claim: we can build a heap from an arb array in O(n) time
							- how? Heapify: Build the heap in place from the bottom up
								- Space Complexity: O(1)
								- Runtime Complexity: O(n)
						- ##### Floyd's Algo
							- Place the leaves in the heap
							- percolate down the first non-leaf element
								- the subtree rooted at that position will be a proper heap
								- the first non-leaf is at (n//2)-1
							- Continue this process for each node up to the root
								- merge a bunch of small ordered heaps into a larger heap
								- visualgo.net/en/heap
							- Runtime Complexity Analysis
								- last n/2 nodes dont perc
								- the next n/4 nodes can perc 1 level
								- the next n/8 nodes can perc 2 levels
								- the next n/16 nodes can perc 3 levels
								- etc...
								- $$\sum^{logn}_{h=0} \frac{n}{2^h}O(h)=...  $$
								- n-1 edges for n nodes
						- #### Implementation
							- ```python
							  def heapify( self, array: list[int]) -> None
								  #set the heaps data
								  self.data = array
								  
								  #first parent node
								  last_parent_node = (self.get_length()//2)-1
								  
								  #for each node up to the root
								  for i in range(last_parent_node, -1, -1)
									  #percolate down
									  self.percolate_down(i)
								  
							  ```
					- #### Heapsort
						- to sort data
						- Simple Approach: heapify the array, the continually call remove()
							- Runtime Complexity:
						- Efficient Approach:
							- sort the array in place
							- divide into two parts
						- the array elements 0..k always forms a heap k..n are sorted in order
							- $0[Heap]k[Sorted]n$
						- First: heapify the array
						- initialize k = (n-1)
						- while k > 0
							- remove the max element (root at index 0)
							- swap it to the end of the array (at index k) Unlike remove(), do not remove the last element. leave it  in place
							- k=k-1
								```python 
								
								def heapsort(array: list[int]) -> list[int]:
									#build the heap
									heap = Heap()
									#put it in heap order
									heap.heapify(array)
									
									#for k = n-1 to 0
									for k in range(heap.get_length() - 1, -1,-1):
										#swap k and 0
										self.swap(0,k)
										#perc down root to k
										self.percolate_down(0,k)
									#return underlying heap data	
									return heap.data
								
								```
								- Complexity
									- O(n) for heapify
									- N interations
									- bro moves too fast
					- Priority Queue comparison
						- insert = put()
						- remove  = get()
						- 

|                  | Insert() | Remove() | Peek() | Size() |
| ---------------- | -------- | -------- | ------ | ------ |
| Unsorted array   |          |          |        |        |
| Partially Sorted |          |          |        |        |
| Fully Sorted     |          |          |        |        |
|                  |          |          |        |        |

# Heap invariants
- Complete Binary Tree
	- filled left to right
	- all levels filled except last level
- Inserts only to end of nodes
	- requires percolation to satisfy Complete BT
- Any node must be less than its parent and greater than its children
	- for max heap
```python
class Heap:

    data: list[int]

  

    def __init__(self) -> None:

        self.data = []

  

    def get_length(self) -> int:

        return len(self.data)

    def insert(self, item: int) -> None:

        self.data.append(item)

        self.percolate_up(self.get_length() - 1)

  

    def remove(self) -> int | None:

        # check to see if there is a root

        if self.get_length() == 0:

            return None

  

        root = self.data[0]

        # swap root with last element in the tree/array

        self.swap(0, -1)

  

        # remove the last element

        self.data.pop()

  

        # percolate root down

        self.percolate_down(0)

  

        # return original root value

        return root

  

    def peek(self) -> int | None:

        if self.get_length() == 0:

            return None

        return self.data[0]

  

    def swap(self, a:int, b:int) -> None:

        self.data[a], self.data[b] = self.data[b], self.data[a]

    def percolate_up(self, index: int) -> None:

        # while the current node is not the root

        while index > 0:

            # calculate the parent index of the node

            parent_index = (index - 1) // 2

            # compare node with parent

            # if child > parent, swap node values

            if self.data[index] > self.data[parent_index]:

                self.swap(index, parent_index)

            # else: end percolation

            else:

                break

            # reset index to parent, since we have swapped values

            index = parent_index

  

    def percolate_down(self, index: int) -> None:

        # iterate until we are past the end of the array
        # to work with heapsort needs to be modified for k 

        while index < self.get_length():

  

            # each iteration, compare to both left and right child

            left = 2 * index + 1

            right = 2 * index + 2 # right = left + 1

            max_index = index

  

            # if left child is greater, swap index with left child

            if left < self.get_length() and self.data[left] > self.data[max_index]:

                max_index = left

  

            # if right child is greater, swap index with right child

            if right < self.get_length() and self.data[right] > self.data[max_index]:

                max_index = right

  

            # if we don't swap, break. The heap invariant is maintained

            if max_index == index:

                break

  

            # update index to the swapped child index

            self.swap(index, max_index)

            index = max_index

  

  

array = [32, 12, 2, 8, 16, 20, 24, 40, 4]

  

heap = Heap()

  

print(heap.data)
```

#heaps #complexity #code