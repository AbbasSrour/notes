## Entities 
Entities are specific objects or things in the mini-world that are represented in the database.
A specific entity will have a value for each of its [[Attributes|attributes]].

Entities are identified by the combination of:
* A partial key of the weak entity type 
* The particular entity they are related to in the identifying entity type

**Entity Types:** Entities with the same basic [[Attributes|attributes]] are grouped or typed into an entity type.

**Entity Set:**  Each entity type will have a collection of entities stored in the database. Entity set is the 
											current state of the entities of that type that are stored in the database.

## Weak Entity Types
An entity that does not have a key attribute, a weak entity must participate in an identifying relationship type with an owner or identifying entity. 

**Weak Entity Set:** An entity set that does not have a primary key is called weak entity set.

