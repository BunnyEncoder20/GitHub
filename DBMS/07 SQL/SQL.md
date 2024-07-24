- Structured Querying Language is essential a language created for 
	- Creating
	- Reading
	- Updating 
	- Deleting 
- data from the database 
- Any RDBMS will use SQL as the baseline through which it will access the data 

- Necessary to follow along in **MySQL workbench** (or just use one of the online ones)
- Cause I've server geek, I'll follow along in my terminal through MySQL shell using the command : 
```cmd
mysql -u root -p
```
- `-u` flag for the user and 
- `-p` flag for the password (never type in the password into the command)
- After this enter the password when prompted.
- You can see the list of the databases by using the command : 
```SQL
show databases;
```

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
- We can also *rename, add and remove* columns using the **ALTER TABLE** command as follows :
```SQL
ALTER TABLE table_name 
RENAME COLUMN old_column_name 
TO new_column_name;
```

```SQL
ALTER TABLE table_name 
ADD COLUMN column_name data_type;
```

```SQL
ALTER TABLE table_name 
DROP COLUMN column_name;
```

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


#### Insert

- **Inserting** into the Table :
```SQL
INSERT INTO bands (name) 
VALUES ('One Direction'),('Napalm Death'),('BlackPink');
```
- Notice that we are using the Table name followed by the column names which we want to insert data into.
- We can insert multiple columns and record in the same command as follows : 
```SQL
insert into albums(name, release_year, band_id) 
values ('Up All Night',2011,1),('Square One',2016,3),('Scum',1987,2);
```
- **NOTE** that the values are all separate tuples. 

---

#### Reading

- **Reading** the records in the Table
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
- We can use alias for column names in the query so that they are more user friendly to read . This is done using the **AS** command
```SQL
SELECT id AS 'ID' , name AS 'Band Name' 
FROM bands;
```
- Notice how the Strings with spaces are placed inside single quotes.

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

- To get only distinct queries inside of our select statement, we can use the **DISTINCT** keyword: 
```SQL
SELECT DISTINCT name FROM albums ;
```

---

#### Update

-  **Updating a Table** we use the **UPDATE** and **SET** command as follows
```SQL
UPDATE albums
SET release_year = 1992;
```
- Be **careful** as the above mistake will update all the rows of the table *albums* to have the release year of 1992. 
- When using update, we must always select the targeted row(s) using the keyword : **WHERE**
```SQL
UPDATE albums
SET release_year = 1992
WHERE id = 10;
```

> Note that **WHERE** is used at the end of multiple different statements to refine the data records which are fetched for the operations.
> Another popular application of it to filter out the records when we are using the **SELECT** command


---

#### Filtering Techniques

- Using **WHERE** command to narrow down searches:
```SQL
select *  from albums
where release_year > 2010;
```
- The above command will only fetch the records of those *release_year*  which are greater than 2010

- Using the **LIKE** keyword to compare data with strings.
	- `%`  represents any string with any characters and of any length. It could be anything.
	- So when we give something like : 
```SQL
SELECT * FROM albums
WHERE name LIKE '%ni%' ;
```
- what we mean to say is that we want all the names which have the string "ni" in them and they can have anything before or after that sub string.

| id  | name              | release_year | band_id |
| --- | ----------------- | ------------ | ------- |
| 1   | Up All Night      | 2011         | 1       |
| 4   | Midnight Memories | 2013         | 1       |

- We can also use **Logical operators** in SQL such as **AND**, **OR**, **NOT**, etc.
```SQL
SELECT * FROM albums
WHERE name LIKE '%ni%' OR band_id = 2;
```

| id  | name                        | release_year | band_id |
| --- | --------------------------- | ------------ | ------- |
| 1   | Up All Night                | 2011         | 1       |
| 3   | Scum                        | 1987         | 2       |
| 4   | Midnight Memories           | 2013         | 1       |
| 9   | Harmony Coruption           | 1990         | 2       |
| 10  | Fear, Emptiness and Despair | 1992         | 2       |
```SQL
SELECT * FROM albums
WHERE release_year < 2010 and band_id = 2;
```

| id  | name                        | release_year | band_id |
| --- | --------------------------- | ------------ | ------- |
| 3   | Scum                        | 1987         | 2       |
| 9   | Harmony Coruption           | 1990         | 2       |
| 10  | Fear, Emptiness and Despair | 1992         | 2       |

- Another way the **WHERE** command can be used is when we want to filter using a certain range , example : between 2 different years.

```SQL
SELECT * FROM albums
WHERE release_year BETWEEN 2010 AND 2015;
```

| id  | name              | release_year | band_id |
| --- | ----------------- | ------------ | ------- |
| 1   | Up All Night      | 2011         | 1       |
| 4   | Midnight Memories | 2013         | 1       |
| 5   | Take me Home      | 2012         | 1       |
| 6   | Four              | 2014         | 1       |
- As we can see all the *release_years* are between the  specified range 
- We can also filter using key words like **IS NULL** or **IS NOT NULL**

```SQL
SELECT * FROM albums
WHERE release_year IS NULL
```


---

#### Delete 

- *Deleting record* from a table is similar to the *select from* statement: 
```SQL
DELETE FROM albums ;
```
- This will delete all the rows from the database (when we do not specify which rows).
- We specify the table and then which record using the **WHERE** command. 
```SQL
SELECT * FROM albums 
WHERE id = 5 ;
```

---


#### Join 

- **JOIN** allows us to combine two different tables together on different properties 
- **JOIN** allows us to explore the relations between the data tables, which is really the highlighting feature of RDBMS.
- A basic **JOIN** statement could be : 
```SQL
SELECT * FROM bands
JOIN albums ON bands.id = albums.band_id;
```
- The table which we *write first* is supposed to be the table on the *left.*  Here the left table is bands.
- The **JOIN** command combines the tables albums and bands and displays those records only when the *id* of the *bands table*, matches the *band_id*  column of the *albums table*.

- There 3 major types of joins : 
	1. **Inner Join**
	2. **Left Join** 
	3. **Right Join**

##### Inner Join 

- It is the default type of **JOIN**
- In fact we do not even need to type **INNER JOIN** in the query, cause just typing **JOIN** is equivalent to **INNER JOIN**
- Given be below are examples of **INNER JOIN** commands :
	- Consider the following tables and we want to find out the active users (the ones which are doing some action)
![[Pasted image 20240722102459.png]]
![[Pasted image 20240722102509.png]]
```SQL
SELECT * 
FROM customer
JOIN event
ON customer.customer_id = event.customer_id;
```
![[Pasted image 20240722105352.png]]
- Note that **SELECT** * will select all the columns from both the tables but we can specify which columns we want as follows : 
```SQL
SELECT customer.customer_id, customer.name, event.action
FROM customer 
JOIN event 
ON customer.customer_id = event.customer_id;
```

 - The Inner Join will only put the row data into the Join table when there is a match between the column values specified in the **ON** statement. (It looks like a intersection between the 2 tables)

##### Left Join

- Left join is when we want the all the data from the left table and the common data between the 2 tables 
- It looks something like this: 
  ![[Pasted image 20240722105936.png]]
- Example: We want see what each user on the customer table is doing. 
![[Pasted image 20240722105822.png]]
- Hence the **LEFT JOIN** for this table would look something like this : 
```SQL
SELECT * 
FROM customer
LEFT JOIN event
ON customer.customer_id = event.customer_id;
```
- Notice that all the rows in the first table are present regardless if they have a match or not in the second table. 
- The columns of the second table are left blank or null for them.


##### Right Join

- **RIGHT JOIN** is like a **LEFT JOIN** but reversed.
- It is not commonly used as any **RIGHT JOIN** can be easily written as a conventional **LEFT JOIN**.
![[Pasted image 20240722110937.png]]
- Consider the Following Tables : 
![[Pasted image 20240722111012.png]]
- If we want to make a **RIGHT JOIN** between the tables event_v2 and action, we ca do it in the following way : 
```SQL
SELECT *
FROM event_v2
RIGHT JOIN action
ON event_v2.action_id = action.action_id;
```
![[Pasted image 20240722111203.png]]


##### Outer / Full Join

- This Join takes all the rows from both the tables regardless if there is a match or not.
- Consider the following table : 
![[Pasted image 20240722111620.png]]
![[Pasted image 20240722111628.png]]
- If we want to perform **FULL JOIN** on these , it would look something like this:
```SQL
SELECT * 
FROM techer
FULL OUTER JOIN student 
ON teacher.age = student.age;
```
![[Pasted image 20240722111800.png]]
- It basically does this by doing a **LEFT JOIN** and then a **RIGHT JOIN** on the tables.


##### UNION

- **UNION** doesn't make tables, just returns a single Column of combines data from different attributes of one or more tables .
- Consider the same Teacher - Student tables from last example: 
![[Pasted image 20240722111620.png]]
![[Pasted image 20240722111628.png]]
If we were to perform a **UNION** on the ages of the student and teachers, it would look something like this : 
```SQL
SELECT age FROM teacher
UNION
SELECT age FROM stuednt;
```
![[Pasted image 20240722112239.png]]
- **Notice** that there are no duplicate records in the resultant column.
- If we want *all* the values of the **UNION** we can use **UNION ALL**
```SQL
SELECT age FROM teacher
UNION ALL
SELECT age FROM stuednt;
```
![[Pasted image 20240722112336.png]]

##### Cross Join

- It doesn't check for any matches.
- It just takes every row in the left table and attaches it to every row in the right table.
- Consider the same tables from previous examples : 
![[Pasted image 20240722111620.png]]
![[Pasted image 20240722111628.png]]
- A **CROSS JOIN** between the columns teacher names and student names would look something like : 
```SQL
SELECT teacher.name student.name
FROM teacher 
CROSS JOIN student;
```
![[Pasted image 20240722112726.png]]




#### Aggregate Functions

1. **AVG** : returns the **average** of that attribute from specified table:
```SQL
SELECT AVG(release_year) FROM albums;
```
![[Pasted image 20240722124047.png]]
2. **SUM** : returns the sum total of the attribute 
```SQL
SELECT SUM(release_year) FROM albums;
```
![[Pasted image 20240722124343.png]]
3. **COUNT** returns the number of instances of that attribute. It is usually used in a query with the **GROUP BY** keyword. 
```SQL
SELECT band_id, COUNT(band_id) FROM albums
GROUP BY band_id;
```
![[Pasted image 20240722125706.png]]

5. **GROUP BY** just groups the rows of same values into a single row.
- But looking at the band id, doesn't give us much info, we need to combine this with the band table to get their actual names.
- We can do that in the following manner which is just combing all the functions we have learned till now:
```SQL
SELECT b.name as Band_Name, COUNT(a.id) as No_of_Albums
FROM bands as b
LEFT JOIN albums as a
ON b.id = a.band_id
GROUP BY b.id;
```
![[Pasted image 20240722130919.png]]



#### Aggregate Filtering 

- Consider a situation where you have to filter the results of a query based on the aggregate function. 
- We cannot simply put a  **WHERE** statement just before the **GROUP BY** statement as **GROUP BY** aggregation will happen always at the end.
- For such situations, we have the **HAVING** keyword. We can use aggregate results in **HAVING** and can use it to filter the results of the **GROUP BY** aggregate: 
```SQL
SELECT b.name as Band_Name, COUNT(a.id) as No_of_Albums
FROM bands as b
LEFT JOIN albums as a
ON b.id = a.band_id
GROUP BY b.id
HAVING No_of_Ablums > 1;
```
- The above query will get us all the Band names and the number of their albums and makes sure that those record include only those bands which are *having* the number of albums > 1.


### SQL Exercise Questions

All the Questions for these are [here](https://github.com/WebDevSimplified/Learn-SQL?tab=readme-ov-file).

Q1. 

