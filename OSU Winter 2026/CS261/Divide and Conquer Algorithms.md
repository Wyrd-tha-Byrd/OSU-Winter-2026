Technique used in Merge Sort and other algos
Divides problem into small sub problems
handles each step individually and then adds them up
# Merge Sort
#mergesort
Sorting a whole array is hard
merging two already sorted arrays is easier
an array of length 0 or 1 is already sorted(base case)
## Plan:
- Divide into two halves
- Recurse to base case of length 1 or 0 
- Merge/Add up to the full sorted list
## Modeling
- Can be visualized as a recursion tree 
- Split in half, then in half, and so on until base case is reached
- Tree height (max recursive calls) $Log(n)$ where n is the items in list
 - Uses $nlog(n)$ in recursive merge sort
	 - always cutting input space in half and O(nlogn) and because of this will always use $\Theta(nlogn)$ 