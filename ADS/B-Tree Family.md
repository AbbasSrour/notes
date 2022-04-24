## B-Tree Family
 _B-tree_ is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, the term is usually used to refer to a class of balanced tree data structures.
* **B-Tree
* **B+Tree
* **B* Tree**  
* **B^link-Tree

## B+ Tree 
A B+ Tree is a self balancing tree data structure that keeps sorted and allows searches, sequential access, insertions, and deletions in **_O(log n)_** . The B+ tree can have more than two children and is optimized for systems that read and write large blocks of data.

### Properties:
* It is perfectly balanced (i.e, every leaf node is at the same depth)
* Every node other than the root, is at least half-full **(M/2)-1 <= keys <= M-1
* Every inner node with k Keys has k+1 non-null children 

### Nodes
Every B+Tree node is comprised of an array of key/value pairs. The Key is derived from attributes that the index is based on. The values will differ based on whether the node is classified inner node or leaf node. The arrays are usually kept in sorted key order.

### Leaf Node Values
* **Record Ids:** A pointer to the location of the tuple that the index entry corresponds to.
* **Tuple Data:** The actual content of the tuple is stored in the leaf node, secondary indexes have to store record id as their value.

### B-Tree vs B+Tree
* The original B-Tree stores keys+ values in all nodes in the tree, thus being more space efficient since each key only appears once in the tree.
* A B+Tree only stores values in a leaf nodes, inner nodes only guide the search process.

### B+Tree Insert 
We first fond the correct leaf node _L_, put the data entry into _L_ in sorted order, if L has enough space we are done, otherwise split _L_ keys into _L_ and new node _L2_, redistributing the keys evenly, copying up middle key and inserting index entry pointing to _L2_ into parent _L_.

### B+Tree Delete
Start at the root,  find leaf node _L_ where entry belongs, then removing the entry, if _L_ is at least half-full, the operation is done. If not and _L_ has only _(M/2)-1_ entries, try to re-distribute, borrowing from sibling (adjacent node with same parent as _L_). If re-distribution fails, merge _L_ and sibling. If merge occurred, must delete entry(pointing to _L_ or sibling) from parent of L.

### Selection Conditions
The DBMS can use a B+Tree index if the query provides any of a the attributes of the search key. Not all DBMSs support this, for hash index, we must have all attributes in search key.
