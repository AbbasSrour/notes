# Use Case Diagram
A [[Use Case Diagram|use case diagram]] is a graphical depiction of a user's possible interactions with a system. A use case diagram shows various use cases and different types of users the system has and will often be accompanied by other types of diagrams as well. The use cases are represented by either circles or ellipses.

Use case diagram is used during [[Requirement Specification|requirements specification]] and analysis to represent external behavior (visible from the outside of the system). 
## Actor:
An actor represents a model or a  role for an external entity, that is, a type of user of the system which interacts with the system, it can be a physical user, external system, or even a physical environment.

An actor has a unique name and an optional description, it is represented by a *stick man*. There are two types of actors:
* **Primary Actor:** Solicits the execution of a use case.
* **Secondary Actor:** Is solicited during the execution of a use case.

### Primary-Secondary
A primary and a secondary actors should not be connected to the same use case, rather the use case should be cut into 2 separate use cases for better clarity. The only exception to that is when solicited actor is an automated external system.

### Inheritance
At all times if an actor A can do all of what an actor B can and has also use cases of its own, then actor A should inherit actor B.

## Use Case Relationships
Use case relationships are relationships between a use case and another use case.
### Extends 
Extends is a use case relationship and is  used when a use case is seldom invoked by another use case or is an optional functionalities. It models a special alternative branch in a use case scenario. 

A use case relationship is represented by a dotted arrow from the extending to the extended use case, i.e if X extends Y then X might be optionally executed by Y,  $X \rightarrow Y$.
**Notes:**
* No extend should be drawn from two use cases of two different actors.

![](https://d3n817fwly711g.cloudfront.net/blog/wp-content/uploads/2015/02/use-case-diagram-relationships-extend.png)

### Includes 
An include relationship is added when a use case is automatically/necessarily triggered by another use case. X includes Y, means that X requires/triggers the execution of Y $X\rightarrow Y$. The include relationship is represented by an arrow form the including to the included.

**Notes:** 
* Their should be no include between a use case and the login use case.
* No include should be no include from two use cases of two different actors.
* 

![](https://www.uml-diagrams.org/use-case-diagrams/use-case-include-split.png)

### Generalize
A generalize use case is when a use case may occur in two or more different ways. X generalizes Y & Z means that X can be preformed as either Y or Z. It typically represents a menu or a sub menu. It is represented by arrows from the generalizations to the generalized.

![](https://i.stack.imgur.com/VThNF.png)

## Use Case:
A use case represents a class of functionality provided by the system.

## Use Case Model 
The set if all use cases that completely describe the functionality of the system.

