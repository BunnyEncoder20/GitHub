- Structured Querying Language is essential a language created for 
	- Creating
	- Reading
	- Updating 
	- Deleting 
- data from the database 
- Any RDBMS will use SQL as the baseline through which it will access the data 

- Necessary to follow along in **MySQL workbench** (or just use one of the online ones)

----

### SQL Syntax 

- Key words 
	- They are several key words : **SELECT, WHERE, FROM**
	- They are not case sensitive : **select, SELECT, SElect**
	- But it is always a standard practice to write all the SQL keywords in *CAPS*
- Command / Query
	- They a bunch of keywords 
	- columns names 
	- Table name
	- At the end there should be a "**;**"
	- Eg: Below query selects all the column from the table "tableName"
```SQL
SELECT * FROM tableName;
```

> Note that when we want to give a string in SQL, we place it inside single quotes : **'string here'** 


---

### Creating a Database

1. Below is the query to create a database : 
```SQL
CREATE DATABASE testDB;
```

> Note that the ⚡ will run either the highlighted query or if nothing is selected, run the entire script file
> Note the ⚡ with with cursor line will execute only the line on which the cursor is on.

 2. Below is the query to remove the database : 
```SQL
DROP DATABASE testDB;
```
- This command removes the entire DB and all of it's tables and records
- We almost never want to use this command 

3. Telling SQL that we want to use our created DB
```SQL
CREATE DATABASE testDB;
USE testDB;
```
- The Database name would be bolded when we are using that database in the MySQL workbench


---

### Tables 

 1. When we want to create a Table we use the **CREATE TABLE** command
```SQL
CREATE TABLE test (
	id INT,
	Col1 INT
);
```
- Remember that the entire CREATE TABLE is a block, hence the semi colon only comes after the it, and not on every line.
- After the column name, we have specified the *Data type* of the column

2. If we want to add another column to the already made table or change any other property of our table, we usually will use : **ALTER TABLE** command 
```SQL
ALTER TABLE test 
ADD Col2 VARCHAR(255);
```
- Notice that though the command is on 2 lines, but it is one single command (hence the ; is only on the second line).
- **ADD** is also another key word 

3. If we no longer have use of the table, we can drop that table using the : **DROP TABLE** command
```SQL
DROP TABLE test;
```

4. We can specify certain properties of the columns in the  tables  such as : 
```SQL
CREATE TABLE test_table(
	id INT NOT NULL AUTO_INCREMENT,
	name VARCHAR(255) NOT NULL,
	PRIMARY KEY (id)
);
```
- The **id** column has the constraint of cannot be null and has a property of auto increment, which basically, automatically assigns the value of id column by  incrementing the previously value when a new record is added.
- The **name** column cannot be empty 
- The **id** column has been made the **Primary Key** of the table.

5. We can also make a **Foreign Key** by as follows : 
```SQL
CREATE TABLE band(
	id INT NOT NULL AUTO_INCREMENT,
	name VARCHAR(255) NOT NULL,
	PRIMARY KEY (id)
);

CREATE TABLE albums(
	id INT NOT NULL AUTO_INCREMENT,
	name VARCHAR(255) NOT NULL,
	release_year INT,
	band_id INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (band_id) REFERENCES band(id)
);
```
- The **Foreign key** is created in a similar way to the primary key.
- The **Foreign Key** specifies 
	- which columns is supposed to the foreign key (Here: band_id of the current table) 
	- which table and column it is supposed to reference (Here: band table and id column of that table)



### CRUD Ops on Tables 

1. **Inserting** into the Table 
```SQL
INSERT INTO bands (name) 
VALUES ('One Direction'),('Napalm Death'),('BlackPink');
```
- Notice that we are using the Table name followed by the column names which we want to insert data into.

2. **Reading** the records in the Table
```SQL
SELECT * TABLE bands;
```
- ⭐ **selects all the columns** from the table and will display all the rows of the Table "band"
- Output : 

| id  | name         |
| --- | ------------ |
| 1   | The Beatles  |
| 2   | Led Zeppelin |
| 3   | Pink Floyd   |
| 4   | Black Pink   |
- We can specify columns we want by modifying the above command 
```SQL
SELECT id,name FROM bands;
```

| id  | name         |
| --- | ------------ |
| 1   | The Beatles  |
| 2   | Led Zeppelin |
| 3   | Pink Floyd   |
| 4   | Black Pink   |

```SQL
SELECT name FROM bands;
```

| name         |
| ------------ |
| The Beatles  |
| Led Zeppelin |
| Pink Floyd   |
| Black Pink   |

- We can limit the number of rows which we want to display by using the **LIMIT** keyword : 
```SQL
SELECT * FROM bands LIMIT 2;
```

| name         |
| ------------ |
| The Beatles  |
| Led Zeppelin |
- We can rename the Column names in the query so that they are more user friendly to read . This is done using the **AS** command
```SQL
SELECT id AS 'ID' , name AS 'Band Name' 
FROM bands;
```

| ID  | Band Name    |
| --- | ------------ |
| 1   | The Beatles  |
| 2   | Led Zeppelin |
| 3   | Pink Floyd   |
| 4   | Black Pink   |
- You can also **order** the way the select statement renders the records using the **ORDER BY** keyword (by defaults makes it **ASC** order)
```SQL
SELECT * FROM bands
ORDER BY name ;
```
- Output : 

| ID  | Band Name    |
| --- | ------------ |
| 4   | Black Pink   |
| 2   | Led Zeppelin |
| 3   | Pink Floyd   |
| 1   | The Beatles  |

- We can also order them in descending order using the **DESC** keyword
```SQL
SELECT * FROM bands
ORDER BY name DESC;
```

| ID  | Band Name    |
| --- | ------------ |
| 1   | The Beatles  |
| 3   | Pink Floyd   |
| 2   | Led Zeppelin |
| 4   | Black Pink   |

