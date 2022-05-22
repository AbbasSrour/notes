# Relational Data Model
The relationship [[DBMS|data model]] is the most widely used model today, it revolves around [[Relationships|relations,]] and is a basically a table with rows and columns. Every relation has a schema, which describes the columns and fields. A *row* (tuple) represents a fact that corresponds to a real world entity or relationship. Each row has a value of an item or set of items that uniquely identifies that row in the table.  Each *column* typically called by its column name or attribute name.

## Attribute Type
Each attribute has a name, the set of allowed values for each attribute is called the *domain* of the attribute. Attribute values are usually required to be atomic (not multi-valued or composite), and a special value **null** is a member of member of every domain, although the null value may cause complications with some operations. The order of tuples are is irrelevant in a database. <br>
* $A_1, A_2, A_3$ ... represent attributes.
* $R(A_1,A_2,A_3...A_n)$   represent the relational schema.
* $r(R)$  is a relation the relational schema $R$.
* $D_1,D_2,D_3...$  are the set of values, where  $r$ a relation is a set of n-tuples $(a_1,a_2,a_3...)$  where $a_i \in D_i$  

## Keys
### Superkey
$K$  is a superkey of $R$  if values for K are sufficient to identify a unique table of each possible relation $r(R)$ .  Superkeys are represented by the name of the attribute underlined.
### Candidate Key
Is the minimal key of $R$ where it can be a superkey of $R$.
### Foreign Key
The foreign key is an attribute X in relations R and s, where it is the primary key of S and not of R. Foreign keys are represented with a # before the attribute name (i.e. **#SSID**) .

## Translating ER to RDM
* Every Entity will be added as a separate table.
* When a relationships between two entities A  (0,1) and B(0,n) exists, we add the primary key of relationship B in A as a foreign key and give it the name of the relationship.
* When a relationship between tow entities A(0,n) and B(0,n) exists, we create a new table with primary keys of the two entities as foreign keys.