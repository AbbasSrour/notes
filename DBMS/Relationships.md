## Relationships
A relationship relates two or more distinct [[Entities]] with a specific meaning. Relationships of the same type are grouped or typed into a relationship type.

**Relationship Type:** Is the schema description of a relationship identifies the relationship name and the participating entity types and also identifies certain relationship constraints.

**Relation Type Degree:** The degree of a relationship type is the number of participating entity types.

**Relationship Set:** The current set of relationship instances represented in the database, and the current state of a relationship type.

**Relationship Type Attributes:** A relationship type can have [[ER Model Diagram#Attributes|attributes]], most relationship attributes are used with M:N relationships. In 1:N relationships, they can be transferred to the entity type on the N-side of the relationship.

## Recursive Relationship
An relationship type whose with the same participating entity type in distinct roles.

## Constraints on Relationships
Constraints on Relationship Types (Also known as ratio constraints) can be:
* **Cardinality Ratio:** specifies maximum participation
	* One-to-one (1:1)
	* One-to-many (1:N) or Many-to-one (N:1)
	* Many-to-many (M:N)
* **Existence Dependency Constraint:** specifies minimum participation
	* zero (optional participation, not existence-dependent)
	* one or more (mandatory participation, existence-dependent)
### Alternative Notation: Min/Max
Specified on each participation of an entity type E in a relationship type R,  which specifies that each entity e in E participates in at least min and at most max relationship instances in R. The default(no constraint): min=0,  max=n (signifying no limit), and it must have min≤max, min≥0, max ≥1.  This notation is derived from the knowledge of mini-world constraints.

## Relationships of Higher Degree
**Binary Relations:** Relationship types of degree 2
**Ternary Relations:** Relationship types of degree 3
**N-Ary Relations:** Relationship types of degree n