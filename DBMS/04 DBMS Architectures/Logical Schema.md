- Defines the DB's structure from a logical or conceptual perspective, without considering how the data is physically stored.
- Concerned with *what kind of data* is stored 

![[logical_schema_tree]]
### Types of Logical Schema 

1. **Conceptual Schema:** represents the overall view of the entire DB. Defines all the high level structure and relationships between all the data elements.
2. **External/View Schema:** defines user-specific views of the DB. Focuses on portions of the DB which are relevant to specific user roles and applications 


### Characteristics of Logical Schema

- It delineates how 
	- data is structured into tables 
	- the interconnections between these tables 
	- and the restrictions placed on data 
- It prioritizes data modelling and DB design over considerations related to hardware or storage specifications
- Examples:
	- Defining tables 
	- specifying primary and foreign keys
	- creating views for data access 