## Attributes 
Attributes are properties used to describe an entity. Each attribute has a value set (or data type) associated with it – e.g. integer, string, sub-range, enumerated type, …
### Types of Attributes:
* **Simple:** Each entity has a single atomic value for the attribute.
* **Composite:** The attribute may be composed of several components.
* **Multi-valued:** An entity may have multiple values for that attribute.
* **Derived attribute:** attributes that can be calculated (derived) from other attributes

**Note:**  In general, composite and multi-valued attributes may be nested arbitrarily to any number of levels, although this is rare. 

### Key Attributes
An attribute of an entity type for which each entity must have a unique value is called a key attribute of the entity type. A key attribute may be composite, and each key is underlined in the ER Diagram.

**Super Key:** A super key of an entity set is a set of one or more attributes whose values uniquely determine each entity. An entity can have only one Super key from the pool of candidate keys.
**Candidate Key:** A candidate key of an entity set is a minimal super key, an entity may have multiple candidate keys.