# Database Design Process
## Conceptual Modeling
After studying the requirements and the needs of the project, the first step in [[DBMS/Database/Database|database]] design is create the conceptual schema of the database through the creation of an [[ER Model Diagram| ER Model]]. 

## Logical Model
After the creation of the conceptual model the ER schema is transformed into a relational schema, where designers may add additional integrity constraints at this stage to reflect real world constraints.

## Normalization
The resulting relational schema is [[Normalization|normalized]] to generate a good schema. Where the schema is tested over example databases to evaluate the quality and correctness, the results are then analyzed and corrections are made to the schema and translated back to the conceptual model to keep the conceptual description of data consistent.

Design tools automate some of the schema transformation, normalization, generation of example database to test the schema design as well as evaluation.