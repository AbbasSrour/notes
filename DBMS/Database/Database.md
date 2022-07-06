## Data Model
A Data Model is a set of concepts to describe the
* **structure**  of a database
* **operations** to manipulate these structures
*  **constraints** that the database should obey

## Constructs And Constraints
### Constructs
Constructs are used to define the database structure, they typically include:
* **Elements** (and their data types) 
* **[[Relationships]]** among such groups 
* **Groups Of Elements** (e.g. [[Entities]], record, table)
### Constraints 
Constraints specify some restrictions on valid data which must be enforced at all times.

## Operations
Data Model operations are used for specifying database retrievals and updates by referring to the constructs of the data model. Operations on the data model may include basic model operations (e.g. generic insert, delete, update) and user-defined operations (e.g. compute_student_gpa,  update_inventory)

## Categories Of Data Models
### Conceptual data models:
Provide concepts that are close to the way many users perceive data. Also called entity based  or object-based data models.
### Physical data models:
Provide concepts that describe details of how data is stored in the computer. These are usually specified in an ad-hoc manner through DBMS design and administration manuals.
### Implementation data models:
Provide concepts that fall between the above two, used by many commercial DBMS implementations (e.g. relational data models used in many commercial systems).

## Schemas
### Database Schema:
The description of a database, includes descriptions of the database  structure, data types, and the constraints on the database.
### Schema Diagram:
An illustrative display of (most aspects of) a database schema.
### Schema Construct:
A component of the schema or an object within the schema, e.g., STUDENT, COURSE.

## Database State
The actual data stored in a database at a particular moment in time.  This 
includes the collection of all the data in the database.

**Initial Database State:**  Refers to the database state when it is initially
loaded into the system.

**Valid State:** A state that satisfies the structure and constraints of the database.

## Three-Schema Architecture
Defines DBMS schemas at three levels:
* **Internal Schema:** At the internal level to describe physical storage structures and access paths (e.g indexes). Typically uses a physical data model.
* **Conceptual Schema:** at the conceptual level to describe the structure and constraints for the whole database for a community of users. Uses a conceptual or an implementation data model.
* **External Schemas:** at the external level to describe the various user views. Usually uses the same data model as the conceptual schema.

Mappings among schema levels are needed to transform requests and data. Programs refer to an external schema, and are mapped by the DBMS to the internal schema for execution. Data extracted from the internal DBMS level is reformatted to match the user’s external view (e.g.  formatting the results of an SQL query for display in a Web page).

## Data Independence
### Logical Data Independence:
The capacity to change the conceptual schema without having to change the  external schemas and their associated application programs.
### Physical Data Independence:
The capacity to change the internal schema without having to change the conceptual schema. For example, the internal schema may be changed when certain file structures are reorganized or new indexes are created to improve database performance. When a schema at a lower level is changed, only the mappings between this schema and higher-level schemas need to be changed in a DBMS that fully supports data independence. The higher-level schemas themselves are unchanged.

## DBMS Languages
### Data Definition Language (DDL):
Used by the DBA and database designers to specify the conceptual schema of a database. In many DBMSs, the [[Data Definition Language|DDL]] is also used to define internal and external schemas (views). In some DBMSs, separate storage definition language (SDL) and view definition language (VDL) are used to define internal and external schemas.
### Data Manipulation Language (DML):
Used to specify database retrievals and updates, [[Data Manipulation Language|DML]] commands (data sub-language) can be embedded in a general-purpose programming language such as COBOL, C, C++, or Java. A library of functions is used to access the DBMS from a programming language. Alternatively, stand-alone DML commands can be applied directly (called a query language).
