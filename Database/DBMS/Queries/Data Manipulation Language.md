# Data Manipulation Language
Used to specify database retrievals and updates, [[Data Manipulation Language|DML]] sql commands (data sub-language) can be embedded in a general-purpose programming language such as COBOL, C, C++, or Java. A library of functions is used to access the DBMS from a programming language. Alternatively, stand-alone DML commands can be applied directly (called a query language).

# SQL
SQL is based on set and relational operations with certain modifications and enhancements. A typical query has the form of: 
```sql
select A1,A2...An
from r1,r2...rn,
where P
```
* **$A_i$** : represents the targeted attributes
* **$r_i$** : represents the targeted relations
* **$P$** : is the predicate

SQL commands can be mapped to [[Relational Algebra#Relational Algebra|relational algebra]] [[Relational Algebra#Operations|operators]].

## Queries
### Select
*SELECT*  is equivalent to  project  $\Pi_{A_1,A_2...A_n}$ , it is used to list the attributes desired in the result of a query.  Select is in the form of:
```sql
select attribute_name1
from r
```
* An asterisk can be used in the select clause to denote all attributes:
```sql 
select *
from r
```
* SQL also allows duplicates in relations as well as in query results, using `select dustinct` forces the elimination of duplicates:
```sql
select distinct attribute_name1
from r
```
* To specify that duplicates should not be removed `select all`  is used:
```sql
select all attribute_name2
from r
```
* The select clause can contain arithmetic expressions, to reformat and modify the data extracted.
```sql
select attribute1, attribute2, attribute3*100
from r
```
**NOTE:** Attributes used in a query must belong to the relations declared in the `from` command. 

### Where 
*WHERE* is equivalent to [[Relational Algebra#Operations#Select|select]]  $\sigma_P(r_1\times r_2 \times r_3...\times r_n)$  in [[Relational Algebra|relational algebra]] and specifies conditions on which tuples of the relation should be extracted. It also allows for arithmetic and logical expressions to be used in the expression. 
```sql
select attribute1
from r
where attribute1="x" and attribute2>y
```
* SQL allows the usage of `between`  which specifies an upper bound and a lower bound for the extracted values.
```sql
select attribute_1
from r
where attribute_n between x and y -- it can be attribute_1 or any other 
                                  -- attribute in r
``` 
**NOTE:** Attributes used in a query must belong to the relations declared in the `from` command. 

### From 
The from clause corresponds to the [[Relational Algebra#Operations#Cartesian-Product|cartesian product]]  $r_1\times r_2$ operation in [[Relational Algebra|relational algebra]], and is rarely used without the `where` command.
```sql
select *
from r1,r2
```
If two attributes across two different relation have the same name, the targeted attribute should be in the form of `r.targeted-atribute` in the `select` statement and the the relations should be aliased in the `where` statement.
```sql
select attribute, relationName1.dupTargetedAttribute
from relationName1 as x, and relationName2 as y
where x.dupTargetedAttribute = y.targetdAttribute ...
```

### Rename
Renaming relations and attributes in SQL is done using the `as` command, when the `as` command is used in the `select` to rename attributes, the change will only effect the outputted data of the result, where as using as in the `from`  command to alias relations, the new names can be used in the other proceeding commands.
```sql 
select attribute1, r1.attribute2 as x
from r1 as relation1, r2 as relation2
where relation1.attribute2 ...
```
* The same table can be aliased two times with different names
```sql
select attribute 
from r as relation1 and r as relation2
where ...
```

### String Operations
Character attributes can be compared to a pattern using the `like` and  `%`  operators, where the `%`  can be used multiple times any position in the pattern.
```sql 
select attribute
from relation
where attribute like "%xyz%abc%" -- the attributes with values in the from 
                                 -- "...xyz...abc..."
```

### Ordering
Ordering of the tuples in the result can be done using the `order by`  command,  with options like `asc` to signify ascending values and `desc` to signify descending value. The operation can have multiple sub-orderings and is  in the form of:
```sql
select attribute1, attribute2
from relation1, relation2
where ...
order by attribute1 asc, attribute2 desc ....
```

### Set Operations
The set operations `union`, `intersect`, and `except` operate on relations and correspond to the relational algebra operations  $\cap,\cup,-$ . Each of the set operations automatically eliminates duplicates, and the usage of `union all`, `intersect all`, and `except all` is needed to retain the duplicates.

The selected attributes from the first expression in the set operation should have the same data type as the ones in the second relation.
```sql
(select attribute1 
from relation1
 where ...)
union --or intersect or except
(select attribute2
 from relation2
 where ...)
```

### Aggregate Functions
SQL has corresponding command to the [[Relational Algebra#Operations#Aggregate Functions And Operations| aggregation functions]]  in [[Relational Algebra|relational algebra]], which is `group by`. Attributes in the select statement appearing before the aggregation function must appear in the `group by` command.
```sql
select attribute1,attribute2...attributen, aggr-function(attributex)
from relation 
group by attribute1, attribute2 ... attributen
```
Most notable aggregation functions:
*  `avg:` average value
*  `min:` minimum value
*  `max:` maximum value
*  `sum:` sum of values
*  `count:` the number of values
The `distinct` and the `*`  operators can be used in the aggregate functions to only use distinct values in the former and to use all the values across all the attributes in the latter.
```sql
select count(distinct attribute), avg(*)
from relation
where ...
```
### Set Membership
$$F\hspace{2mm}in\hspace{2mm}r\iff \exists \hspace{1mm}t \in r(t=F)$$
$F$ is an attribute name and the set of values is typically returned by the sub-query.

#### in
The operator `in`  signifies that the data needed resides in a relation `x`. 
```sql
select attributeX
from relationX
where attributeX in (select attributeX from relationY)
```
#### some
The `some` clause means that if a value exists in the set of values of $F$ then the statement will be true otherwise it will be false. 
#### all
The `all` clause returns true if and only if the comparison is true for all elements of relation x, and false otherwise.


### Nested Sub-Queries
Every SQL statement returns a relation/set in the result, which can be anything ranging from [[Null|null]] to a single atomic value; this means that values can be replaced with an SQL statement. Nested operations are illegal if the returned value has a different data type to do the one it is being operated on with.
```sql
select *
from relationX
where attributeX > (select avg(attributeY) from relationY)
```
### Division
Division is an [[Relational Algebra#Division|relational algebra expression]] and can be translated into sql for R(A,B,C,D) and S(C,D) by using the query:
```sql
create view v as
	select A,B,S.C,S.D
	from R, S
		except 
	select A, B, C, D 
	from R
select A, B from R expcept select A,B from v
```
  Another way to create division operation for R(A,B) and S(B) is:
```sql
Create view v as
	Select A, S.B
	From R as R1, S
	where not exists(select A, B
									 from R
									 where A=R1.A and B=S.B)
Select distinct A
from R
where not exists (select *
									from v
									where R.A=v.A)
```

## DB Modification
### Deletion
To delete a rows from a relation the `delete` command is used. If `where` is not used then all the data will be deleted.
```sql
delete from relationX
where <query>
```
### Insertion
To add a new tuple in a relation, the `insert into` command is used, with the values of the tuples. To reorder the attributes, the attribute names must be specified.
```sql
insert into relationX(attributeX,attributeY,attributeZ)
values(valueX, valueY, valueZ)
```
We can add values using sql queries, where the attributes selected should be compatible with the relation inserted into.
```sql
insert into relationX -- can include (attributeA, attributeB, attributeC)
select attributeY, attributeZ, X
from relationY
where ...
```
### Update
`Update` is an sql command to change the values of a tuple, is is used in combination with a command `set`.
```sql
update relationX
set relationX = X;
where ...
```
### Modifying DB With Views
It is allowed to modify the data of a database using a [[Views|views]], but it becomes exponentially difficult and complex as a view gets more complex, hence updating a database using complex views is not allowed.