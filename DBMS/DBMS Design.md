## Design Decisions
### Issues
* **Data Organization:** How to layout data structures in memory/pages and what information to store to support efficient access.
* **Concurrency:** How to enable multiple threads to access the data structure at the same time without causing problems.

## Table Indexes
A table index is a replica of a subset of a table's attributes that are organized and/or sorted for efficient access using a subset of those attributes.
The DBMS ensures that the contents of the table and the index are logically in sync. 

It is the DBMS job to figure out the best indexes to use to execute each query. There is a trade-off on the number of indexes to create per database. 

## Clustered Indexes 
The table is stored in the sort order specified by the primary key, which can either be heap or index organized storage. Some DBMS always use a clustered index, but if the table doesn't contain doesn't contain a primary key, the DBMS  will automatically  make a hidden row id primary key.

## Data Structures
Data structures can be used for multiple design decisions to store things like:
* **Internal Meta-Data:**  Usually use [[Hash Tables]].
* **Core Data Storage:** Usually use [[Hash Tables]].
* **Temporary Data Structures:** Usually use [[Hash Tables]].
* **Table Indexes:** Usually use [[B-Tree Family#B Tree|B+Tree]].

## [[Hash Tables]] Design Decisions
In DBMS we want fast hash tables that have low collision rates, and we don't care about cryptographic features.

## [[B-Tree Family#B Tree|B+Tree]] Design Decisions 
### Node Size 
1. **Storage Type:** The slower the storage device, the larger the optimal node size for B+Tree:
	* **HDD** ~ 1 MB
	* **SSD** ~ 10 KB
	* **In Memory** ~ 512 Bytes
2. **Workload Type:** Optimal sizes can vary depending on the workload
	* **Leaf Node Scans:** Larger node sizes are better because it is sequential IO workload.
	* **Root-To-Leaf Traversal:** Smaller node sizes are better because it is  random IO workload.

### Merge Threshold
Some DBMSs do not always merge nodes when it is half full, delaying a merge operation may reduce the amount of recognition. It may also be better to just let under-flows to exist and then periodically rebuild entire tree.

### Variable Length Key
Different DBMSs use different approaches to handle variable length keys:
* **Pointers:** Stores the keys as pointers to the tuple's attribute, uses less space but slow and expensive for look-ups.
* **Variable Length Nodes:** The size of each node in the index can vary, but requires careful memory management.
* **Padding:** Always pad the key to the max length of the key type.
* **Key Map:** Embed an array of pointers to map to the key+value list within the node.

### Non-Unique Indexes 
Their are two ways to handle non unique indexes :
* **Duplicate Keys:** Use the same leaf node layout but store duplicate keys multiple times.
* **Value Lists:** Store each key only once and maintain a linked list of unique values.

### Intra-Node Search
* **Linear:** Scan node keys form the beginning to end.
* **Binary Search:** Jump to middle key, pivot left/right depending on comparison.
* **Interpolation:** Approximate location of desired key based on known distribution of keys.

### Prefix Compression
Sorted keys in the same leaf node are likely to have the same prefix, instead of sorting the entire key each time, extract common prefix and store only unique suffix for each key.

### Suffix Truncation 
The Keys in the inner nodes are only used to direct traffic, thus we don't need the entire key. So the suffix truncation is an optimization procedure where we store a minimum prefix that is needed to correctly route probes into the index.

### Bulk Insert
The fastest/best way to build a B+Tree is to first sort the keys and then build the index from the bottom to the top.

### Pointer Swizzling
Nodes use page ids to reference other nodes in the index, the DBMS must get the memory location from the page table during traversal, which is expensive. We can mitigate this if the a page is pinned in the buffer pool we can store raw pointers instead of page ids. This avoids address lockups from the page table.

### Duplicate Keys
There are two approaches to handle duplicate keys in a DBMS:
* **Append Record Id:** Add the tuple's unique record id as part of the key to ensure that all keys are unique, the DBMS will also be still be able to use partial keys to find tuples.
* **Overflow Leaf Nodes:** Allow leaf nodes to spill into overflow nodes that contain duplicate keys, this approach makes it more complex to maintain and modify.


## Index Usage
### Implicit Indexes
Most DBMSs automatically create an index to enforce integrity constraints but not referential constraints(foreign keys).

### Partial Indexes 
Create an index on a subset of the entire table, this potentially reduces its size and the amount of overhead to maintain it. One common use case is to partition indexes by date ranges.

```sql
CREATE INDEX idx_foo
ON foo (a,b)
WHERE c = 'x';
```

### Covering Indexes 
If all the fields needed to process the query available in an index then the DBMS does note need to retrieve the tuple. This reduces contention on the DBMS buffer pool resources.
```sql
CREATE INDEX idx_foo
ON foo (a,b);
```

### Index Include Columns
Embed additional columns indexes to support index only queries, these extra columns are only stored in the leaf nodes and are not part of the search key.

### Functional/Expression Indexes
An index does not need to store keys in the same way that they appear in their base table.
```sql 
CREATE INDEX idx_user_login
ON foo (x)
WHERE EXTRACT(y from x);
```

### Inverted Index
An inverted index stores a mapping of words to records that contain those words in the target attribute.

## Trie Tree
A trie tree uses digital representation of keys to examine prefixes one-by-one instead of comparing entire key, also known as Digital Search Tree or Prefix Tree.

### Properties
* Shape only depends on key space and lengths, insertion order, pre-existing keys don't influence the shape.
* Doesn't need re-balancing.
* All operations are O(k) where k is the length of the k, the path to the leaf node represents the key of the leaf node, keys are stored implicitly and can be reconstructed from paths.

### Trie Key Span
The span of a trie is the number of bits that each partial key/digits represents, if the digit exists in the corpus then a pointer to the next level in the trie branch is stored, otherwise it stores null.
This determines the fan-out of each node and the physical height of the tree.

### Radix Tree
The radix tree is a variation of the trie tree which omits all nodes with only one single child, can produce false positives, so the DBMS always checks the original tuple to see whether a key matches. 

### Query Types
* **Phrase Searches:** Find records that contain a list of words in the given order.
* **Proximity Searches:** Find records where two words occur within n words of each other.
* **Wildcard Searches:** Find records contain words that match some pattern 

 ### Design Decisions
 * **Storage:**  The index needs to store at least the words contained in each record, separated by punctuation characters, in addition to that it can store frequency, position, meta-data... 
 * **Update:** Maintain auxiliary data structures to stage updates and then update the index in batches.