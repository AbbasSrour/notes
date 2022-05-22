# Data Definition Language:
Used by the DBA and database designers to specify the conceptual schema of a database. In many DBMSs, the [[Data Definition Language|DDL]] is also used to define internal and external schemas (views). In some DBMSs, separate storage definition language (SDL) and view definition language (VDL) are used to define internal and external schemas.

#tldr
In other words the DDL is responsible for the implementation of the database design, and the creation of a database containing the schema for each relation, the domain of values associated with each attribute, the integrity constraints, the set of indices to be maintained for each relation, security and authorization information for each relation, and the physical storage structure of each relation.

## Domain Types
### Types
The type of values that an attribute will have, the most common types used are:
* **char(n):** Fixed length string, with user specified length n.
* **varchar(n):** Variable length character string, with user-specified maximum length n.
* **int:** integer.
* **smallint:** small integer.
* **real:** Floating point and double-precision floating point numbers, with machine dependent precision.
* **float(n):** Floating point number, with user specified precision of at least n digits.
* **date:** Dates, containing a 4-digits year, month, and day
* **time:** Time of day, in hours minutes and seconds.

### Null
Null values are allowed by default, and using the `not null` command will prohibit null values for that attribute.

### Domain Creation
The DDL allows for the creation of custom domains with custom names using the basic provided domains, using the `create domain` command.
```sql
create domain <domain-name> char(20) not null
```

## Table Creation
An sql relation is defined using the `create table` command:
```sql
create table r ( A1 D1,
								 A2 D2,
								 A3 D3,
								 ...,
								 An Dn,
								 
								 <integrity-constraint1>,
								 <integrity-constraint2>,
								 ...,
								 <integrity-constraintk>
								)
```
Where `r` is the relation name, $A_i$ is the attribute name,  and $D_i$ is the domain of $A_i$.

### Integrity Constrains
Integrity Constraints are **the protocols that a table's data columns must follow**. These are used to restrict the types of information that can be entered into a table. This means that the data in the database is accurate and reliable. You may apply integrity Constraints at the column or table level. Primary key for example is an integrity constraint because it must always must be unique, or a check on the values entered for an attribute like being $check(attrinute_j > x)$.
