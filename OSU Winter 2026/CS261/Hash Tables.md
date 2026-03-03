Unique key per item in hash table
Hashes out addressing efficiently compared to a large array 

## Operations
#### Runtime Complexity O(1)
- insert(key,value) - insert new value at key
- remove(key) - remove the value and key
- get(key) - Return the value for key
- contains(key) - Check if key exists
- length() - return number of items in table
## Properties
- Key is the unique name of the address, can be any datatype as long as it is unique
- Value can be anything, like a full student/employee record
- Every key has an associated value
- basically a big array under the hood 
# Dictionaries
- Built into python as {}
	```python
	name = {} 
	name[jdawg123] = 'user a'
	name[dfsd] = 'user b'
	name[hgfhg] = 'user c'
	```
# Hash Functions
A good hash function should be able to return unique 
```python
def hash_function(string: str) -> int:
	sum = 0
	for char in string:
		sum += ord(char)
	return sum
```
## Collisions
- Example: if hashing strings, a simple hash function may sum of ordinal ascii values
- needs handling for all cases
	```python
	hash(x)==hash(y) # collision
	
	hash(x) % capacity == hash(y) % capacity # collision
	```
### handling methods
- #### Chaining
	- Instead of storing a single value for each index store a list of keys and values
	- append new data to the end of the list for each index
	- increases time complexity to O(n)
	- ```python
  def insert(self, key: str, value: str) -> None:
	  index= hash(key) % self.capacity
	  bucket = self.data[index]
	  for entry in bucket:
		  if entry.key == key:
			  entry.value = value
			  return
		bucket.append(Entry(key, value))
		
		
def remove(self., key: str) -> None:
	index = hash(key) %self.capacity
	bucket = self.data[index]
		for i in range(len(bucket)):
			 del bucket[i]
			 
	  ```
- #### Probing
	- has many schemes
		- linear probing $(probe+1)$
		- quadratic $(probe + i^2 + i * j) for i=0...n-1$
		- double hashing 
	- Similar to how we implement chaining
	- probe next bucket while index is not empty, when empty is found, insert
	- Removals with open addressing will return None when a bucket with different bucket than its hash value is removed and then searched for
		- ##### Solution: Tombstones
			- Instead of deleting data, replace it with a tombstone that tells you what used to be there
			- can be written over with new data as long as the hash bucket is not empty
	- Problems:
		- Clustering - Linear Probing can cause a pile up on keys if the hash values are are similar
			- Scan further ahead with quadratic
		- Load Factors $O(x)$
			- Using open addressing a tables load factor cannot exceed 1
				- low load factors -> avoid collisions
				- low load factor -> a lot of unused space
				- Larger hash table = more computationally efficient at the cost of memory
## Hashing
- Used in more places than just hash tables
	- cryptography and security rely on hash values to ensure message integrity 
		- cryptographic hashes: sha256, md5
	- passwords are stored as hashes rather than directly in databases
	- hashing is a very popular topic of mathematical research

- Hash tables usually want a lighter weight and faster algorithm
	- ### Determinism
		- required - given input maps to the same hash function value
	- ### Uniformity
		- The inputs should be mapped as evenly as possible over the output range
			-  A non-uniform function can resullt in many collisions via clustering
			- is good distribution of values to keys
	- ### Speed
		- the function should have a low computational burden
- Methods
	- Folding
		-  Hash(x) maps key x to any integer in the entire output space
		- many different techniques to accomplish
			- Summing all elements
				- not sufficient by itself for uniformity
			- Multiplying all elements
				- not sufficient by itself for uniformity
	- Shifting 
		- To fix the issues of folding, we can use shifting which increases the coeff  by a power of 2
			- $$2^0, 2^1, 2^2,...$$
			- Can get as complex as necessary for security
	- DJB Hash
		- ```python
		  def hash (string: str) -> int:
			  hash_value = 5381
			  for c in string:
				  hash_value = (hash_value << 5) + hash_value + ord(c)
				return hash_value
		  ```
		  - Generally works regardless of the string
		  - fast, deterministic algorithm with good uniformity
  - Perfect and minimally perfect Hash Functions
	- Hash collision: some keys map to the same index:
		- x != y but hash(x) == hash(y)
		- A perfect hash function is one that results in no collisions
		- A minimally perfect hash function is one that results in no collisions for a table size that exactly equals the number of elements
			- common when you hash involves a specific data domain, e.g. student IDs or license plate numbers 
- Build your own hash function
	- If we create a custom class, we often need to specify how to calculate its hash value
	- Python default = memory reference
		- it is guaranteed unique: hash(x) != hash(y)
		- but not transitive: hash(x) != hash(y) even when x == y
	- Most languages have built in support
	- when defining a class, we often want to provide a custom hash function
		- which attributes are important to:
			- Include
			- Exclude
		- Immutability: hash values should remain consistent even if data changes
	- ```python
	class Student:
		  name: str
		  id: int
		  gpa: float
		  current_classes: list[str]
		def __hash__(self) -> int:
			return hash((self.name, self.id))
		def __eq__(self,other) -> bool:
			return self.name == other.name and self.id == other.id
  
	def hash_demo() -> None:
		student = Student()
		student.name = "Benny Beaver"
		student.id = 934123456
				  
	  ```

### Sets - Practice problem

  ```python
  def two_sum(input: list[int], sum: int) -> bool:
	  sums = {}
	  for a in input:
		  sums[a] = 1
	  for a in input:
		  b = sum - a
		  if b in sums:
			   print(f"({a}+ {b} = sum")
			   return True
	  return False
  ```
  - Set functions like a dictionary 
	  - unique - no dupes
	  - unordered - cannot access items in index value
  - Key operations:
     - is an element contained in the set
     - equivalent to a mathematical set
     - Every operation runs in constant time O(1)
     - union() - return the union of the two sets
	     - can also be used in the form '(A | B)'
	     - or A.union(B)
	 - intersection() - given two sets, returns the intersection (common elements)
		 - (A )
	 - difference() - 
		 - (A - B)
	 - symmetric_difference() - return the set of all elements in either A or B not both
		 - (A ^ B)
- Uses:
	- path finding
	- caches
	- finding common values across multiple data sources
	- finding unique values
- Python built in set type:
	- set()
- 😭😭
#hashing #hashtables #complexity #code