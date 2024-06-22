
# Hibernate

### What is hibernate?
- Hibernate is an open-source and lightweight ORM tool that is used to store, manipulate, and retrieve data from the database.

### What is ORM?
- ORM is an acronym for Object/Relational mapping.
- It is a programming strategy to map object with the data stored in the database. 
- It simplifies data creation, data manipulation, and data access.

### Define persistent classes.
- Classes whose objects are stored in a database table are called as persistent classes.

### What is SessionFactory?
- SessionFactory provides the instance of Session. It is a factory of Session. 
- It holds the data of second level cache that is not enabled by default.
### Is SessionFactory a thread-safe object?
- Yes, SessionFactory is a thread-safe object, many threads cannot access it simultaneously.

### What is Session?
- It maintains a connection between the hibernate application and database.

- It provides methods to store, update, delete or fetch data from the database such as persist(), update(), delete(), load(), get() etc.

- It is a factory of Query, Criteria and Transaction i.e. it provides factory methods to return these instances.

### Is Session a thread-safe object?
- No, Session is not a thread-safe object, many threads can access it simultaneously. 
- In other words, you can share it between threads.