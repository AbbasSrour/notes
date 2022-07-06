# Normalization 
The normalization process is done after the creation of the [[ER Model Diagram|conceptual]] and [[Relational Data Model|relational]] schema, and testing the design in example databases to evaluate the correctness and quality of the design. 

The normalization process decomposes the relational schema to remove redundancy and remove anomalies. Results in semantically equivalent relational schema that the represents the same information as the original. 

## Schema Refinement And Normal Forms
Conceptual design gives us a set of relation schema and integrity constraints that can be regarded as a good starting point for the database final design. The initial design is then refined by taking into consideration the integrity constraints and the functional dependencies more fully, and also by considering the performance criteria and typical workloads.

## Redundancy 
Redundancy is storing the information redundantly in more than one place within a database, which can lead to several problems when the design is implemented and the database is used in the final project.

Intuitively, redundancy arises when relational schema forces association between attributes that is not natural.

Problems caused by redundancy:
* **Redundant Storage:** Some information is stored repeatedly which can lead to the database becoming bigger in size then it needs to.
* **Update Anomalies:** If one copy of such repeated data is updated, an inconsistency is created.
* **Insertion Anomalies:** It may not be possible to store some information unless some other information is stored as well.
* **Deletion Anomalies:** It may not be possible to delete some information without losing some other information as well.

## Decomposition 
Decomposition is the replacing of a relation with a collection of smaller relations$\{ R_1, R_2, R_3...R_n\}$ such that each relation $R_i$  is in good form and the decomposition is a lossless-join decomposition. Decomposition is used to solve the problem of redundancy, where each smaller relation contains a subset of the attributes of the original relation.

All attributes of the original schema must appear in the decomposition of the relation, where $R=R_{1}\cup R_2$ . And the combined data of the new relations must be equal to that of the old schema as a result of a lossless-join decomposition  $r=\Pi_{R_1}(r)\Join \Pi_{R_2}(r)$. 

## Functional Dependencies
In relational database theory, a functional dependency is a constraint between two sets of attributes in a relation from a database where the value of one depends on the value of the other. 

The use of functional dependencies is to test relations if they are legal or not, where relations are legal under a set F, if r satisfies $F(F|=r)$ . Another use of functional dependencies is to specify constraints on the set of legal relations, we say that F holds on R if all legal relations on R satisfies the set of functional dependencies F.

### Keys: An Alternative Definition
#### Super Keys
K is a super key for relation schema R if and only if $K\rightarrow R$ .

#### Candidate Key
K is a candidate key for R if and only if $K\rightarrow R$, and their is no  $\alpha\subset K, \alpha\rightarrow R$. 

#### Minimal Keys
Any attribute which does not appear in the right member of a non trivial functional dependency of F must be belong any key (candidate or minimal) of R. If the set of the attributes of R which do not appear in right member of a non trivial FD of F is a key, then R possess an unique minimal key formed of the set of these attributes.

### Closure
Given a set of functional dependencies F, there are certain other functional dependencies that are logically implied by F. The set of all functional dependencies logically implied by F is the closure of F, we denote the closure of F by $F^+$ . 

We can find all of F+ by applying Armstrong's Axioms .

#### Armstrong's Axioms
We can find all of F+ by applying Armstrong's Axioms . For $\alpha ,\beta , \hspace{1mm} \gamma$ sub set of attributes the Armstrong's Axioms are:

* **Reflexivity:** if $\beta \subseteq \alpha$,  then  $\alpha \rightarrow \beta$ . 
* **Augmentation:** if $\alpha \rightarrow \beta$, then  $\gamma \alpha \rightarrow \gamma \beta$.
* **Transitivity:** if $\alpha\rightarrow\beta$  and $\beta\rightarrow\gamma$, then $\alpha\rightarrow\gamma$.
* **Union:** if $\alpha\rightarrow\beta$ and $\alpha\rightarrow\gamma$, then $\alpha\rightarrow\beta\gamma$ .
* **Decomposition:**  if $\alpha\rightarrow\beta\gamma$ then $\alpha\rightarrow\beta$  and $\alpha\rightarrow\gamma$.
* **Pseudo Transitivity:** if $\alpha\rightarrow\beta$  and $\gamma\beta\rightarrow\delta$,  then  $\alpha\gamma\rightarrow\delta$ .

#### Closure Of Attribute Sets
The closure of $\alpha$  under $F$ denoted by $\alpha^+$  as the set of attributes that are functionally determined by $\alpha$ under F.
$$\alpha\rightarrow\beta\hspace{2mm}is\hspace{2mm}in\hspace{2mm}F^+ \iff\beta\subseteq\alpha^+$$
 
The algorithm to compute $\alpha^+$, the closure of $\alpha$  under $F$:

$$
\begin{gathered}
\hspace{2cm}while(change\hspace{2mm}to\hspace{2mm}\alpha^+)\hspace{2mm}do\\
\hspace{4cm}for\hspace{2mm}each\hspace{2mm}\beta\rightarrow\gamma\hspace{2mm}in \hspace{2mm} F\hspace{2mm}do\\
Begin\\
\hspace{5cm}if\hspace{2mm}\beta\subseteq\alpha^+\hspace{2mm}then\hspace{2mm}\alpha^+=\alpha^+\cup\gamma\\
End\\
\end{gathered}
$$

### Canonical Cover
