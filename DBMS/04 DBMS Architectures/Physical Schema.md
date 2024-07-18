- A physical schema defines how the data is stored in underlying hardware 
- Concerned about where the data is actually (physically) stored 
- includes details like : 
	- storage formats
	- file organization 
	- indexing methods
	- data placement 
	- Methods of storage (BTree method, hashing)

### Characteristics of Physical Schema

- Primarily focus lies in enhancing the storage and retrieval of data to boost performance
- Modification of physical schema demand meticulous planning and potentially affect the overall performance of the DB
- `Example :` deciding to use clustered indexes on certain columns for faster retrievals.