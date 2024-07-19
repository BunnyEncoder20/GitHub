- **Intension** defined what kind of data can be stored and the relationships between them
	- Blue print or the definition of the DB structure 
	- **Doesn't frequently change** and is **the permanent** definition of the DB structure 
- It includes : 
	- *Tables Definitions* (name of the table, their columns, data types allowed in each columns) 
	- *Constraints* (Rules that govern the data, such as primary , foreign keys, validation rules)
	- *Relationships between the tables* (how the tables are connected through shared columns)
- Example given : 
```
customer(
id INT PRIMARY KEY,
name VARCHAR(50)
)
```
---

- **Extension** is the actual data stored in the database at a given instance in time. 
- Basically the data which is stored in *tuples* at a given instance of time.
- When there is more data added, the data **can change**.