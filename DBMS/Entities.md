## Entities 
Entities are specific objects or things in the mini-world that are represented in the database.
A specific entity will have a value for each of its [[Attributes|attributes]].

Entities are identified by the combination of:
* A partial key of the weak entity type 
* The particular entity they are related to in the identifying entity type

**Entity Types:** Entities with the same basic [[Attributes|attributes]] are grouped or typed into an entity type.

**Entity Set:**  Each entity type will have a collection of entities stored in the database. Entity set is the 
											current state of the entities of that type that are stored in the database.

## Weak Entity Set
An entity that does not have a key attribute, a weak entity must participate in an identifying relationship type with an owner or identifying entity. We underline the discriminator of a weak entity set with a dashed-line.

### Identification Relation
Identifying Relationship is a relationship between a strong and a weak entity type, where the key of the strong entity type is required to uniquely identify instances of the weak entity type. The weak entity type will have a partial key attribute that, in conjunction with the key of the strong entity type, uniquely identifies weak entity instances.

## Specialization
We designate sub-groupings within an entity set that are distinctive from other entities in the set.These sub-groupings become lower-level entity sets that have attributes or participate in relationships that do not apply to the higher-level entity set. Thus the lower-level entity set inherits all the attributes and relationship participation of the higher-level entity set to which it is linked.

![](https://static.studytonight.com/dbms/images/specialization.jpg)

## Generalization
**Generalization** is a bottom-up approach in which two lower level entities combine to form a higher level entity. In generalization, the higher level entity can also combine with other lower level entities to make further higher level entity.

![](https://static.studytonight.com/dbms/images/generalization.jpg)

## Aggregation
Aggregation is a process when relation between two entities is treated as a **single entity**.
In the diagram above, the relationship between **Center** and **Course** together, is acting as an Entity, which is in relationship with another entity **Visitor**.

![](https://static.studytonight.com/dbms/images/aggregration.jpg)
