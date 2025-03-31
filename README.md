# HashTablesNotes

Challenge: spellchecker with near real time processing
- Unsorted list $O(n)$ time (too slow)
- Sorted list, binary search $O(\log_{2}n)$ (still too slow)
- We want like 1 comparison (or a set number so it doesn't increase so much)

Hash Table
- A data structure that can map keys to values (key-value pairs)
- It uses a hash function to compute an index (or hash code) into an array of buckets (or slots), from which the desired value can be found

Hash Function
- Takes a key as input and returns an integer (the hash code (where the key will go))
- Goal is to distribute keys evenly across the buckets
	- Figures out where to put new data entries

Properties of a Good Hash Function
- Deterministic: not random, the same key always produces the same hash code
- Uniform Distribution: Keys should be spread evenly across the range of possible hash codes to minimize collisions.
	- To make data useful
	- To not overwhelm servers/drives/systems
	- To use all resources uniformly and maximally
- Efficient to Compute: It should be a fast function, otherwise there is no point in using a hash table
- Avalanche Effect: A small change in the key should result in a large change in the hash code

Collisions
- When two different keys produce the same hash code, they map to the same bucket
- This is unavoidable, especially as the has table fills up, since the hash function isn't bijective (injective specifically)
- Collision resolution is extremely important

Collision Resolution Strategies
- Separate Chaining: Each bucket stores a linked list (or another dynamic data structure) of key-value pairs that hash to that bucket. When a collision occurs, the new key-value pair is simply added to the linked list.
- Open Addressing: All key-value pairs are stored directly in the array. When a collision occurs, we probe for an empty slot using a specific strategy.
	- Linear Probing: If a collision occurs at index $i$, we try $i+1$, then $i+2$, etc., wrapping around to the beginning of the array if necessary.
		- The Avalanche Effect helps with this as indexes immediately after elements should be empty. 
	- Quadratic Probing: If a collision occurs at index $i$, we try $i+1^2$, then $i+2^2$, then $i+3^2$, etc. (using modulo for the table size to avoid overflow).
	- Double Hashing: Uses a second hash function to determine the probing interval. If a collision occurs at index $i$ we try $i+(1*h{2}(key))$, then $i+(2*h{2}(key))$, etc.

Real-World Applications of Hash Tables
- Databases: used for indexing in databases, allowing for fast lookups of records based on keys
- Caches: (like in web browsers or operating systems) uses to determine if data is already stored. The key might be a URL and the value would be the cached content
- Programming Languages (Dictionaries/Maps): Many programming languages provide built-in hash table implementations
	- e.g., dict in Python, HashMap in Java, map in C++
- File Systems: Some file systems use hashing to quickly verify fire integrity or find duplicate files

Hash Table Advantages
- Fast Average-Case Performance: $O(1)$ (constant) for insertion, deletion, and lookup (on average, with a good hash function and low load factor)
- Efficient Key-Value Storage: Provides a natural way to associate keys with values

Hash Table Disadvantages
- Worst-Case Performance: $O(n)$ if all keys hash to the same bucket (degenerate case)
	- This is why good hash function design and collision resolution are so important
- Unordered: Hash tables to do maintain the order of insertion
	- If you need ordered data, a hash table is not the right choice (consider a tree-based structure like a balanced binary search tree)
- Hash Function Design: Choosing a good hash function can be tricky and depends on the nature of the keys
	- There is no universal hash function
- Space Overhead: Hash tables require extra space for the buckets, even if they are not all used. Resizing can also be expensive
