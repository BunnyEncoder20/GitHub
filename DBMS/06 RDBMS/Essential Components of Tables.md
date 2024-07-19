- **Row/Tuples** : rows - aka tuples or records, represent individual entities or instances of data within the table
- **Cardinality** : Number of rows in the table 
- **Column/Attributes** : Columns represents the attributes of the data being stored and are named to describe the information they hold 
- **Degree** : The number of columns in a table

---

- **Constraints**  :  define rules or conditions which must be satisfied by the data in the table
	- Common constraints include uniqueness, nullability, default values, etc.
		- *Unique constraints* : Ensure the values of this column are unique across the table
		- *Not Null constraint* : Ensure that this column cannot be left empty 
		- *Check constraint* : Ensure that a condition is true for all the records of the column 
		- *Default values* : if no value is specified, provides a default value
- [[Keys in DBMS]] : 
	- **Primary Key :** is a **unique identifier for each** record in the table. It ensures the row can be identified and accessed within the table.
	- **Foreign Key** : is a column of a table which *refers the primary key of another table*. It is used to establish relation between tables.