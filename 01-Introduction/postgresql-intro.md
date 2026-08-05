# Introduction: (POSTGRES, post-gres-ql, (ingres->post ingres))
- opne Source RDBMS

React Frontend -> Node.js Backend -> PostgreSQL Database

# Why choose PostgreSQL instead of another database?
- with this we get full ACID compliant(it esnure maximum acid compliance)
- completely free, opne source, very reliable, hanlde huge data, strong security, advanced feature(it can act as both traditonal relational db or document oriented db), excellent performance


# How PostgreSQL Fits in Full Stack
- Browser  React -> HTTP Request -> Node.js / Express -> SQL Query -> PostgreSQL -> Stores Data

# when to choose postgresql
- when data has clear relationship
- needs high consistency
- require complex querying

| Feature        | PostgreSQL               | MongoDB                                   |
| -------------- | ------------------------ | ----------------------------------------- |
| Database Type  | Relational (SQL)         | NoSQL (Document)                          |
| Data Format    | Tables (Rows & Columns)  | JSON-like Documents                       |
| Schema         | Fixed/Structured         | Flexible                                  |
| Relationships  | Excellent                | Possible but less natural                 |
| JOIN Support   | Powerful                 | Limited compared to SQL joins             |
| Transactions   | Very strong (ACID)       | Supported, but traditionally less central |
| Query Language | SQL                      | MongoDB Query Language                    |
| Best For       | Structured business data | Flexible, evolving data                   |




DBMS
Stores and manages data.
Relationships are not a core requirement.
RDBMS
A type of DBMS.
Stores data in related tables.
Uses primary keys and foreign keys.
Ensures data integrity with constraints and transactions.
SQL
A language used to query and manipulate data.
PostgreSQL
An RDBMS.
Uses SQL as its primary language.
Stores, manages, secures, and retrieves data efficiently.
One-line summary

SQL is the language you write, PostgreSQL is the software that executes it. PostgreSQL is an RDBMS, and every RDBMS is a specialized type of DBMS.
