- **Keys**  in is a attribute in table which make sure of data integrity, uniqueness and the quick retrieval of data
- Types of keys : 
	- [[Primary Key]] : is a **unique identifier for each** record in the table. It ensures the row can be identified and accessed within the table.
	- [[Foreign Key]] : is a column of a table which *refers the primary key of another table*. It is used to establish relation between tables.
	- [[Candidate Key]] : It is set of attributes which can act as primary keys for the table
	- [[Super Key]] : set of one or more candidate keys or attributes which can unique identify each row of table

---


### Referential Integrity 

- **Referential Integrity** is a important concept of foreign key. 
	- We always say that *foreign key* maintains referential integrity
- *Referential Integrity* ensures that relations between tables remain accurate, consistent and meaningful throughout the database.
	- The table which is being *referenced* is called **Referenced/Base Table**
	- The table which is *referencing* another table is called **Referencing Table**


### CRUD Operations in Referenced/Base Table

1. **Insertion in Referenced/Base Table**
	- This doesn't affect the *Referencing Table*, hence no violations.
2. **Deletion in Referenced/Base Table**
	- This may cause violation if the corresponding data is present in the *referencing table*
	- If the record of the *referenced table* are deleted, then the corresponding data from the referencing table should also be deleted. 
	- This is necessary to maintain the integrity of the data
		- We use actions like "**CASCADE DELETE**" for the same
		- We could also set null to the values which were deleted.
3.  **Updation in the Referenced/Base Table** 
	- May cause violation if the corresponding data is present in the *referencing table*
	- We can use actions like "**CASCADE UPDATE**" 


### CRUD Operations in Referencing Table

1. **Insertion in Referencing Table**
	- This will cause violation because the record may or may not be present in the *referenced table*
2. **Deletion from the Referencing Table**
	- This will not cause any violation 
3. **Updation in the Referencing Table**
	- No issues as long as the attribute we are updating is not the foreign key.
	- If we are updating the foreign key then it will cause violation.
---

### Integrity Constraints in DBMS

 - **Integrity constraints** helps to ensure that data remains reliable and meaningful throughout the Lifecycle
 - These are *set of rules* which need to be followed before updating and insertion of any kind.
- There are several types of Integrity Constraints 
	- *Domain Integrity constraints* (Eg: check if date column has valid date)
	- *Entity Integrity constraints* (Eg: ensure all records are unique by making primary key always there)
	- *Referential Integrity constraints* (Ensures that the Foreign key and the Primary key it is referencing always match)
	- *Key constraint* (makes sure that there is at least one attribute which can be primary key)
	- *Check constraints* (ensure that the insertion and updation are follow certain conditions else they are rejected)
	- *Null constraints* (determines which attribute columns can accept null values)
	- *Unique constraints* (ensures that values in attribute or group of attribute are unique across the table)
	- *Default constraints* (it ensure that some default value is inserted if no value is provided)