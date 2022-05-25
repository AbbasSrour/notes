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
[[Null]] values are allowed by default, and using the `not null` command will prohibit null values for that attribute.

### Domain Creation
The DDL allows for the creation of custom domains with custom names using the basic provided domains, using the `create domain` command.
```sql
create domain <domain-name> char(20) not null
```
## Database Creation
To create a database and allocate a space for it the `create database` command is used, to specify the name of the database and the location of the database and the log file.
```sql
USE master
GO
CREATE DATABASE <database-name>
ON (NAME=\<database-name>_dat,
		FILENAME = '/location/of/<database-name>.mdf')
LOG ON (NAME = '/<database-name>_log',
				FILENAME ='/location/of/\<database-name>.ldf')
GO
```
Using pSQL:
```sql
create database <db-name> owner <owner-name> tablespace <tablespace-name>;
```


## Table Creation
An sql relation is defined using the `create table` command:
```sql
create table r ( A1 D1 <integrity-constraint>...,
								 A2 D2 <integrity-constraint>...,
								 A3 D3 <integrity-constraint>...,
								 ...,
								 An Dn <integrity-constraint>...,
								 
								 <integrity-constraint1>,
								 <integrity-constraint2>,
								 ...,
								 <integrity-constraintk>
								)
GO
```
Where `r` is the relation name, $A_i$ is the attribute name,  and $D_i$ is the domain of $A_i$.

### Integrity Constrains
Integrity Constraints are **the protocols that a table's data columns must follow**. These are used to restrict the types of information that can be entered into a table. This means that the data in the database is accurate and reliable. You may apply integrity Constraints at the column or table level. Examples of integrity constraints:
* **primary key(`<attribute-name1>, <attribute-name2>...<attribute-namek>`)** 
* **foreign key(`<attribute-name>`) references `<table-name>`(`<referenced-attribute>`)**
* **check(P)**
* **not null/null**
* **constraint `<constraint-name>` `<constraint1>`. . .`<constraintk>` (`<attribute-name>`)**
* **unclustered/clustered**

## Drop And Alter Table
### Drop
To delete a table from database the command `dop table` which deletes the schema and the tuples of a relation.

### Alter
The  `alter table r` command in conjunction with `add <attribute-name>` or `drop <attribute-name>` is used to modify an existing relation.

