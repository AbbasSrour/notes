# Relational Algebra
Relational algebra is a [[Formal Languages#Pure Languages|pure]] [[Formal Languages#Query Languages|procedural language]] with 6 basic operations that take two or more relations as inputs and give new relation as result.

# Operations
## Select
$$\sigma_p(r) = \{\hspace{2mm}t \hspace{2mm}| \hspace{2mm} t \in r\hspace{2mm} and \hspace{2mm} p(t)\hspace{2mm}\}$$
Where $p$ is called the selection predicate, a formula in propositional calculus consisting of terms connected by $\land$, $\lor$,  and  $\lnot$ in the form of: 

$\lt attribute \gt$ $binary$ $relation$  $\lt attribute\gt$ or $\lt constant\gt$.

And $r$ is the relation selected.

## Projection
$$ \Pi_{A_1,A_2...A_K} (r)$$
Where $A_1,A_2...A_K$ is are the attribute names and $r$ is the relation name.

The result of the operation is the defined as the relation of k columns obtained by erasing the columns that are not listed, and duplicate rows are removed from result since relations are sets.

### Generalized Projection
$$ \Pi_{F_1,F_2,F_3..nF_n}(r)$$
Generalized projection generalizes the projection operation by allowing multiple arithmetic functions to be used in the projection list.


## Union
$$ r\hspace{1mm}\cup\hspace{1mm}s\hspace{2mm} = \hspace{2mm} \{ \hspace{2mm} t \hspace{2mm} | \hspace{2mm}t\in r \hspace{2mm} or\hspace{2mm} t \in s \hspace{2mm} \}$$
For the union to be valid the two tables $r$ and $s$  should have the same number of attributes and the attribute domain must be compatible. The final table has no duplication if the two tables have identical tuples.

## Set Difference 
$$ r - s \hspace{2mm}=\hspace{2mm}\{ \hspace{2mm} t \hspace{2mm}|\hspace{2mm} t\in r \hspace{2mm} and \hspace{2mm} t\not\in s \hspace{2mm} \}$$
For the operation to be valid the two tables should be compatible, meaning that the tuples should have the same number of attributes with the domain of the attribute domain must be compatible.

![](https://s33046.pcdn.co/wp-content/uploads/2020/01/two-set-difference-in-set-theory.png)


## Cartesian-Product
$$ r \times s \hspace{2mm} = \hspace{2mm}\{ \hspace{2mm} t, \hspace{1mm} q \hspace{2mm}|\hspace{2mm} t\in r \hspace{2mm} and\hspace{2mm} q \in s \hspace{2mm} \}$$
This operation assumes that the attributes of $r(R)$ and $s(S)$ are disjoint, i.e.  $R \cap S\hspace{1mm} = \phi$  . If not then renaming must be used.

## Set Intersection 
$$ r \cap s \hspace{2mm} = \hspace{2mm} \{\hspace{2mm} t \hspace{2mm}|\hspace{2mm} t\in r \hspace{2mm} and \hspace{2mm} t \in s \hspace{2mm} \}$$
The operation assumes that the tables are compatible, i.e. they have the same number of attributes and the attribute domain must be compatible.

**Note:** $r\cap s\hspace{2mm}=\hspace{2mm} r-(r-s)$ 

## Rename & Assignment
### Rename
$$\rho_x(E) $$
It returns expression $E$ under the name $x$, this allows us to name the results of an operation by more than one name.

### Assignment 
$$temp \hspace{2mm} \leftarrow \hspace{2mm}E$$

The assignment operation provides a convenient way to express complex queries by sorting intermediate results into temporary relations, assignment must always be made to a temporary relation variable.


## Join
### inner
$$ r\Join s$$
For r and s, relations on schemas R and S, the result of a natural join is a schema $R\cup S$  which is obtained by considering each pair of tuples tr from r and ts from s. If tr and ts have the same value on each of the attributes in $R\cap S$, a tuple t is added to the result, where t has the same value as tr on r and the same value of ts on s.
The join operation can be defines as$$\Pi_{r.A,r.B,r.C,s.E}(\sigma_{r.B=s.B,r.D=s.D}(r\times s))$$

where $R = (A, B,C, D)$  and $S=(E,B,D)$.

### outer
$$A ⟕ B$$
An extension of the join operation that avoids loss of information, it computes the join and then adds tuples in the other relation to the result of the join. It uses null to signify that value is unknown or does not exist.

## Division
$$ r \div s \hspace{2mm}=\hspace{2mm}\{\hspace{2mm}t\hspace{2mm}|\hspace{2mm}t\in\Pi_{R-S}(r)\hspace{2mm}\land \hspace{2mm} \forall u\in s(tu\in r)\hspace{2mm}\}$$
The division operation can also be defined as:
$$ r\div s \hspace{2mm} = \hspace{2mm} \Pi_{R-S}(r)-\Pi_{R-S}((\Pi_{R-S}(r)\times s)-\Pi_{R-S,S}(r))$$
## Aggregate Functions And Operations
$$_{G_1,G2...G_n} g_{F_1(A_1),F_2(A_2)...F_n(A_n)}(E)$$
Where $g$ is an algebraic operation, $G_1,G_2...G_n$ are the attributes on which to group, $F_i$ is the aggregate function and $A_i$ is an attribute.

Aggregation functions take a collection of values and returns a single value as a result, some basic aggregation functions are:
* **avg:** The average value
* **min:** The minimum value
* **max:** The maximum value
* **sum:** The sum of the values
* **count:** The number of values

The value of an aggregate function doesn't have a name, and can be names using the *as* keyword: $_{G_1}g_{F_1 \hspace{2mm}as\hspace{2mm}x }(E)$

## Deletion
A delete request is expresses similarly to a query, expect instead of displaying tuples to the user, the selected tuples are removed. Only he whole tuples are deleted, and individual values can't.
$$r\leftarrow r-E$$
## Insertion
To insert data into a relation we either specify a tuple to be inserted or we write a query whose result is a set of tuples to be inserted. The tuples must be compatible with table and the operation is in the form : $$r\hspace{1mm}\leftarrow \hspace{1mm} r \hspace{1mm} \cup \hspace{1mm}E$$
## Updating
A mechanism to change a value in a tuple without changing all the values of a tuple, with the operation having the form of:$$r\hspace{1mm}\leftarrow \hspace{1mm} \Pi_{F_1,F_2,F_3...F_n}(r)$$
Where $F$ it either the $i_{th}$ attribute of $r$, and $F_{i}$ is an expression, involving only constants and attributes of r, which gives the new value for the attribute.

## Expression Relations 
A basic expression in the relational algebra consists of either a relation in the database or a constant relation, and operations can be used on two different expressions like $\cup,\hspace{2mm}\cap, \hspace{2mm}- , \hspace{2mm}\times,\hspace{2mm}\sigma_p(E),\hspace{2mm} \Pi_s(E), \hspace{2mm}\rho_x(E)...$ 

## Composite Of Operations 
Building expressions from two or more operations.