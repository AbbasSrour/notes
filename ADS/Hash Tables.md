## Hash Tables
A hash table implements an unordered associative array that maps keys to values, it uses **hash functions** to compute an offset into the array for a given key, from which the desired value can be found with complexity  *O(1)*  to *O(n)*. Hash functions have a trade-off between being fast vs collision rate.

### Hashing Scheme
A hash scheme handles key collision after hashing, and the trade-off between allocating a large hash table vs additional instructions to find/insert keys.

### Static Hash Table
Allocate a giant array that has one slot for every element you need to store, to find an entry the function  mods the key by the number of elements to find the offset in the array. Static hash tables need the size  to be declared on creation and each key is unique. 

### Hash Functions
* **CRC64:** Used in networking and error detection.
* **MurmurHash:** Designed to a fast general purpose function.
* **Google CityHash:** Designed to be faster for short keys (<64 bytes).
* **Google FarmHash:** Newer version of City Hash with better collision rates.
* **Facebook XXHash:** From the creator if zstd compression, __V3__ is considered the best hashing function as of 2019.

## Static Hashing Schemes
### Linear Probe Hashing 
Single giant table table of slots, it resolves collisions by linearly searching for the next free slot in the table, insertions and deletions are generalizations of look-ups. 

* __Deletion Methods:__
	* **Tombstone:** If an element a logical value is put in place of the deleted value that tells the program to consider it as non-empty on lockups.
	* **Movement:** It moves all the elements under the deleted key in the table one position up.

*  **Collisions:** 
	* **Separate Linked List:** Store values in separate storage area for each key.
	* **Redundant Keys:** Store duplicate keys entries together in hash table.

### Robin Hood Hashing
Variant of linear probe hashing that steals slots from *rich* keys and give them to *poor* keys, each key tracks the number of positions they are from where its position in the table, on insert a key take the slot of another key if the first key is farther away from its optimal position than a second key.

### Cuckoo Hashing
Use multiple hash tables with different has function seeds, on insert check every table and pick that has a free slot, if no table has a free slot evict the element from one of them and then rehash it find a new location, look ups and deletions are always *O(1)* because only one location per has table is checked.


## Dynamic Hash Tables
### Chained Hashing 
Maintain a linked a linked list of buckets for each slot in the hash table, resolve collisions by placing all elements with same key into the same bucket. Look-ups are done through hashing to the element location and scanning the bucket for it, deletions and insertions are generalized look-ups.  

### Linear Hashing 
The hash table maintains a pointer that tracks the next bucket to split, when any bucket overflows, split the bucket at the pointer location. Uses multiple hashes to find the right bucket for a given key, and can use different overflow criterion like space utilization and average length of overflow chains.