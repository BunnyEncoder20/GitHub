- In a 3-Tier Architecture, there is *another layer between the client and the server*. 
- The client does not directly communicate with the server. Instead, it interacts with an **application server** which further communicates with the database system and then the query processing and transaction management takes place.
- This *intermediate layer acts as a medium* for the exchange of partially processed data between the server and the client. 
- This type of architecture is used in the case of large web applications. 

![DBMS 3-Tier Architecture](https://media.geeksforgeeks.org/wp-content/uploads/34-1.png)
### Advantages of 3-Tier Architecture

- ***Enhanced scalability***: Scalability is enhanced due to the distributed deployment of application servers. Now, individual connections need not be made between the client and server.
- ***Data Integrity:***  Since there is a middle layer between the client and the server, data corruption can be avoided/removed.
- ***Security:***  This type of model prevents direct interaction of the client with the server thereby reducing access to unauthorized data.


### Disadvantages if 3-Tier Architecture 

- ***More Complex Data***: 3-Tier Architecture is more complex in comparison to 2-Tier Architecture . Communication Points are also doubled in 3-Tier Architecture. 
- ***Difficult to understand and interact***: It becomes difficult for this sort of interaction to take place due to the presence of middle layers.
- ***Costly to deploy and maintain***: These big architectures are costly to deploy and maintain. 