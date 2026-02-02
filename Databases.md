# Definition

A **Database** is an organized collection of structured information, or data, typically stored electronically in a [[Operating System|computer system]]. 

While a simple text file can store data, a database is designed to handle large volumes of information, allow multiple users to access it simultaneously, and ensure the data remains accurate and secure.

# The [[DBMS]] 

It is important to distinguish between the **database** (the data itself) and the **[[DBMS]]** (the software used to manage it). 

>The DBMS serves as an interface between the database and the end-user or application, ensuring that data is consistently organized and easily accessible.

- **Common DBMS Examples:** [[MySQL]], [[PostgreSQL]], [[MongoDB]], Microsoft SQL Server, and Oracle Database.

# Relational vs. Non-Relational Databases

The most fundamental division in the database world is between **SQL** and **NoSQL**.

## Relational Databases

Relational databases organize data into **tables** with predefined relationships. 

>They use **Structured Query Language ([[SQL]])** for writing and querying data.

---

- **Structure:** Data is stored in rows (records) and columns (attributes).

- **Key Concept:** **[[ACID]] Compliance**, which guarantees that database transactions are processed reliably (Atomic, Consistent, Isolated, Durable).

- **Best For:** Financial systems, inventory management, and applications where data consistency is the top priority.

### The Power of Keys

The "relational" part comes from how tables connect using **keys**:

**[[Primary Key]]**: A unique identifier (like a barcode or Social Security number) that identifies a specific row in its own table. Every row must have one, and it cannot be empty ([[Null]]).

**[[Foreign Key]]**: A Primary Key from one table that appears in another table to create a link. For example, an OrderID in an "Orders" table might include a CustomerID to show exactly who placed that order.

### ACID Properties

Relational databases follow the [[ACID Principles]] to ensure data stays accurate even during power failures or system crashes:

- **[[Atomicity]]**: Transactions are "all or nothing"—either everything completes or nothing does
- **[[Consistency]]**: Data must follow predefined rules and constraints
- **[[Isolation]]**: Multiple transactions don't interfere with each other
- **[[Durability]]**: Once data is saved, it stays saved permanently

### When to Use Relational Databases

- Most applications (if you're not sure, start with a relational database)
- Applications requiring reliable and accurate information
- Applications needing fast, flexible reporting capabilities
- [[CRUD Applications]] (Create/Read/Update/Delete)

> [!NOTE] Not well suited for
> 
> - Applications processing extreme amounts of data
> - Applications requiring loosely structured information

## Non-Relational Databases 

NoSQL databases are "non-tabular" and store data differently than relational tables. 

>They are designed for flexibility and massive scaling.

---

- **Document Stores:** Store data in [[JSON]]-like structures (e.g., [[MongoDB]]).

- **Key-Value Stores:** Simple "dictionary" style storage (e.g., [[Redis]]).

- **Wide-Column Stores:** Optimized for large datasets (e.g., Cassandra).

- **Best For:** Big Data, real-time web apps, content management, and social media feeds where data structures change frequently.

### Key Characteristics

**Flexible Schema**: You don't need to define a strict structure before adding data. One record can have different fields than the next.

**[[Horizontal Scalability]]**: Instead of making one server bigger ([[Vertical Scaling]]), you can easily add more servers to a cluster.

**High Performance**: Optimized for specific data models (like simple lookups), they can be much faster than relational databases for certain tasks.

### When to Use Non-Relational Databases

- **Your data is unpredictable**: Data changes shape frequently or includes diverse types (images, text, numbers)
- **You need massive scale**: Millions of users or terabytes of data that a single SQL server couldn't handle
- **Speed is the priority**: Lightning-fast reads for simple data models (like a real-time leaderboard)

### Types of Non-Relational Databases

**[[Key-Value Stores]]**: Simple lookup databases

- [[DynamoDB]]
- [[Redis]]

**[[Wide Column Stores]]**: Optimized for large-scale analytical queries

- [[Apache Cassandra]]
- [[HBase]]

**[[Document Stores]]**: Store data as JSON-like documents

- [[Couchbase]]
- [[Firebase]]
- [[MongoDB]]

**[[Graph Databases]]**: Optimized for relationship-heavy data

- [[Neo4j]]

**[[Search Databases]]**: Optimized for full-text search

- [[Elasticsearch]]
- [[Solr]]
# How Databases Work

## [[Indexing]]

An index is a data structure that improves the speed of data retrieval operations. 

>Think of it like the index at the back of a textbook; instead of scanning every page (a "Full Table Scan"), the database looks up the index to find exactly where the data lives.

## [[Querying]]

This is the act of requesting information from the database.

- **SQL Example:** `SELECT name FROM users WHERE age > 21;`

- The [[DBMS]] parses this request, finds the data, and returns it to the application.

## [[Schema]]

A schema is the "blueprint" of the database. 

- In [[SQL]], the schema is rigid (you must define columns before adding data). 

- In NoSQL, the schema is often "dynamic" or "schema-less."

# Database Architecture in the Cloud

Modern databases often move away from a single server to more complex setups:

- **[[Replication]]:** Copying data across multiple servers so that if one fails, the data isn't lost.

- **[[Sharding]]:** Breaking a very large database into smaller, faster pieces (shards) spread across multiple servers.

- **[[Managed Databases]]:** Services like AWS RDS or Google Cloud SQL where the provider handles the backups, patching, and scaling, so the developer only focuses on the data.

# Common Misconceptions

- **"Excel is a database":** While Excel stores data, it lacks the concurrent access, security, and complex relationship-handling of a true DBMS. It is a spreadsheet, not a database.

- **"NoSQL is always better/faster":** NoSQL is better for _scaling_ and _flexibility_, but SQL is often faster and safer for complex queries and highly structured data.

- **"Data is lost if the power goes out":** Because databases use **Persistent [[Storage]]** and transaction logs, they can recover their state even after a crash.

# The Transaction Log

A secret to database reliability is the **Write-Ahead Log ([[WAL]])**. 

Before the database actually changes a value in a table, it writes the intended change to a simple, fast log file. 

>If the system crashes mid-update, it reads the log to finish the job or undo the partial change.

# Related Notes

- [[SQL vs NoSQL Comparison]]

- [[Data Integrity and Constraints]]

- [[Normalisation]]

- [[Caching and Redis]]

- [[Big Data Analytics]]

# Tags

#databases #sql #nosql #data #backend #software-engineering