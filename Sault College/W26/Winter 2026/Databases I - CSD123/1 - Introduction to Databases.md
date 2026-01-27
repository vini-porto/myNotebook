
---
A **database** is a structured collection of related data. Think of it as a highly efficient digital filing cabinet that lives on a computer. While you might use a spreadsheet like Excel for simple lists, databases are designed to handle massive amounts of data and allow you to find, update, or connect pieces of information almost instantly.

## Why Databases Matter
Databases are a core component of most modern information systems:

- **Web applications and websites** - storing user accounts, content, and settings
- **Mobile apps** - managing app data and user information
- **Desktop applications** - organising local data efficiently
- **Web browsers** - storing bookmarks, history, and cache

They provide a **robust way to store information** that is:

- **Fault tolerant** - can recover from crashes and errors
- **Data integrity enforcing** - ensures data follows rules and remains accurate
- **Powerful for analysis** - using query languages like [[SQL]]

## The Problem with Spreadsheets

Imagine you run a dog-walking business and track everything in a spreadsheet with columns like: Client Name, Phone Number, Dog Name, and Walk Date.

This approach leads to three critical **modification problems** (also called **anomalies**):

### 1. The Updating Problem

**Problem**: What if Bob gets a new phone number?

When client information is repeated across multiple rows (because Bob has multiple dogs or multiple walks), you must update every single instance of Bob's phone number. This is:

- **Error prone** - you might miss some instances
- **Creates inconsistency** - if you miss some, you won't know which number is correct later

**Root cause**: [[Redundant Data]] makes updates difficult and unreliable.

### 2. The Inserting Problem

**Problem**: How do you record information for clients whose dogs you haven't walked yet?

If you add just client information without walk data:

- You have **awkward blank cells**
- You must decide where to put these rows (beginning? end? mixed in?)
- Adding a second dog for an existing client requires **repeating all their contact information**

**Root cause**: Storing information about multiple entities (clients, dogs, walks) in a single table makes insertion awkward and redundant.

### 3. The Deleting Problem

**Problem**: What happens if you delete a row after realising the walk didn't actually happen?

When you delete the walk record:

- You **accidentally delete the client information** too
- Or you leave awkward empty cells if you only delete some fields

**Root cause**: Deleting rows from a table that stores multiple types of information can remove more data than intended.

## The Solution: Multiple Tables

The answer to modification problems is **breaking data into multiple related tables**. This process is called [[Normalization]].

### Example: Three-Table Structure

Instead of one large table, create three separate tables:

**Clients Table**

| ClientID | Client Name | Phone Number |
| -------- | ----------- | ------------ |
| 02039    | David       | 2494578854   |

**Dogs Table**

| DogID | Dog Name | ClientID |
| ----- | -------- | -------- |
| 22341 | Derbie   | 02039    |

**Walks Table**

| WalkID | DogID | Walk Date  |
| ------ | ----- | ---------- |
| 17235  | 22341 | 2026-06-01 |

### How This Solves the Problems

**Updating**: Stuart's phone number? Change it in one place in the Clients table.

**Inserting**: New client who hasn't had a walk yet? Just add them to the Clients table with no walks needed.

**Deleting**: Remove a walk that didn't happen? Delete from the Walks table only—client and dog information remains safe.

**Viewing all data together**: If you need to see everything in one big table, [[SQL]] (the language of relational databases) allows you to combine these tables in virtually any way you want.

## Types of Databases

### Relational Databases (SQL)

A [[Relational Database]] stores and organizes data points that are related to one another. It structures data into **tables** (also called **relations**) consisting of rows and columns—like a collection of digital spreadsheets that can "talk" to each other.

#### How Relational Databases Are Organized

**Tables**: Each table represents an [[Entity]] (e.g., "Customers" or "Products")

**Columns (Fields)**: Define the category of data, such as "Customer Name" or "Email"

**Rows (Records)**: Each row is a unique entry in the table (e.g., a specific customer)

#### The Power of Keys

The "relational" part comes from how tables connect using **keys**:

**[[Primary Key]]**: A unique identifier (like a barcode or Social Security number) that identifies a specific row in its own table. Every row must have one, and it cannot be empty ([[Null]]).

**[[Foreign Key]]**: A Primary Key from one table that appears in another table to create a link. For example, an OrderID in an "Orders" table might include a CustomerID to show exactly who placed that order.

#### ACID Properties

Relational databases follow the [[ACID Principles]] to ensure data stays accurate even during power failures or system crashes:

- **[[Atomicity]]**: Transactions are "all or nothing"—either everything completes or nothing does
- **[[Consistency]]**: Data must follow predefined rules and constraints
- **[[Isolation]]**: Multiple transactions don't interfere with each other
- **[[Durability]]**: Once data is saved, it stays saved permanently

#### When to Use Relational Databases

**Well suited for:**

- Most applications (if you're not sure, start with a relational database)
- Applications requiring reliable and accurate information
- Applications needing fast, flexible reporting capabilities
- [[CRUD Applications]] (Create/Read/Update/Delete)

**Not well suited for:**

- Applications processing extreme amounts of data
- Applications requiring loosely structured information

#### Data Integrity in Relational Databases

Relational databases enforce three types of [[Data Integrity]]:

**[[Entity Integrity]]**: No primary key can be empty (null), ensuring every row is unique and identifiable.

**[[Domain Integrity]]**: Data must be the correct type—you can't put a name in a "Phone Number" column.

**[[Referential Integrity]]**: You cannot have a Foreign Key that points to a Primary Key that doesn't exist. This prevents "orphaned" data.

#### Popular Relational Databases

**Server-based:**

- [[MS SQL Server]]
- [[MySQL]] (or [[MariaDB]])
- [[Oracle Database]]
- [[PostgreSQL]]

**File-based:**

- [[Microsoft Access]]
- [[H2 Database]]
- [[MS SQL Express]]
- [[SQLite]]

### Non-Relational Databases (NoSQL)

A [[Non-Relational Database]] (often called [[NoSQL Database]], meaning "Not Only SQL") stores data in formats other than traditional rows and columns. Think of it as more flexible—like a collection of folders or varied documents rather than rigid spreadsheets.

#### Key Characteristics

**Flexible Schema**: You don't need to define a strict structure before adding data. One record can have different fields than the next.

**[[Horizontal Scalability]]**: Instead of making one server bigger ([[Vertical Scaling]]), you can easily add more servers to a cluster.

**High Performance**: Optimized for specific data models (like simple lookups), they can be much faster than relational databases for certain tasks.

#### When to Use Non-Relational Databases

Consider a non-relational database when:

- **Your data is unpredictable**: Data changes shape frequently or includes diverse types (images, text, numbers)
- **You need massive scale**: Millions of users or terabytes of data that a single SQL server couldn't handle
- **Speed is the priority**: Lightning-fast reads for simple data models (like a real-time leaderboard)

#### Types of Non-Relational Databases

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

## Relational Database Management Systems (RDBMS)

An [[RDBMS]] is the complete system that manages relational databases. It's the middleman between users and the raw data, ensuring that when you ask for information, you get it quickly and accurately.

### Components of an RDBMS

An RDBMS consists of four main components:

#### 1. The Relational Database

The actual collection of related data files, consisting of:

- **[[Schema]]**: The structure or skeleton (table definitions, relationships, constraints)
- **Data**: The actual information stored in the tables

The database is usually stored as one or more files. **Important**: You should never manually edit these files—always access them through the [[DBMS]].

#### 2. Database Management System (DBMS)

The [[DBMS]] is the system of programs that enables the management and execution of all aspects of an RDBMS. It's the "engine" that interprets and executes database commands.

**Server-based DBMS**: Consists of a server listening for [[SQL]] commands (e.g., [[PostgreSQL]] Server, [[MySQL Server]])

**File-based DBMS**: Usually consists of a single shell or code library that interprets SQL (e.g., [[SQLite]], [[H2 Database]])

#### 3. Applications

Applications are programs used to interact with the database:

**[[Database Management Applications]]**: Used to create, analyze, and manage databases

- [[DBeaver]]
- [[MySQL Workbench]]
- [[MS SQL Management Studio]]
- [[pgAdmin]]

**User Applications**: Used by end-users to perform application-specific tasks, storing and retrieving data from the database. May communicate with multiple databases.

#### 4. Users

Users interact with applications and have **permissions/roles** that govern how they may interact with the system. RDBMSs support **[[Multi-User Access]]**: many people can read and write to the database simultaneously without conflicts or data corruption.

### RDBMS vs DBMS

**DBMS** (Database Management System) is the software—the "engine."

**Database** is the actual collection of related data files.

**RDBMS** is a specific type of DBMS designed to manage relational data in tables.

**Important distinction**: A DBMS is NOT a database management application.

**Example**: [[PostgreSQL]] is an RDBMS that consists of:

- **PostgreSQL Server** (the DBMS)
- **[[pgAdmin]]** (a database management application for PostgreSQL)
- **[[DBeaver]]** (a database management application that can connect to various DBMSs, including PostgreSQL)

## Common Database Application Architectures

### Desktop / Embedded Applications

In this architecture, the application and database run on the same machine:

- Application connects directly to a file-based DBMS
- Examples: [[Microsoft Access]], [[SQLite]], [[H2 Database]], [[MS SQL Express]]
- Common for single-user applications or small-scale systems

### Enterprise Applications

In this architecture, multiple applications connect to a centralized database server:

- Multiple users and applications access the same database simultaneously
- Server-based DBMS handles concurrent access
- Examples: [[MS SQL Server]], [[MySQL]], [[PostgreSQL]], [[Oracle Database]]
- Common for business applications with many users

### Web Applications

**Architecture**:

- **Front end**: Browser displays the user interface
- **Back end**: Server runs application logic
- **Database**: Stores application data

Multiple browsers connect to the same server, which manages all database interactions.

### Mobile Applications

**Architecture**:

- **Front end**: Mobile app provides the user interface
- **[[API Server]]**: Handles requests from mobile apps
- **Database**: Stores application data

Multiple mobile apps connect to an API server, which acts as an intermediary to the database.

## Summary

At a certain level of complexity, data in a system is best represented by multiple related tables rather than a single list. This approach:

- **Eliminates modification problems** present in single-table designs
- **Reduces redundancy** through normalization
- **Enforces data integrity** through keys and constraints
- **Enables powerful analysis** through SQL queries

**Key points**:

- [[Relational Databases]] are suitable for most applications
- [[Non-Relational Databases]] are useful when processing extreme amounts of data or when data structure is not well-defined
- An [[RDBMS]] consists of Databases, DBMS, Applications, and Users
- Databases are a fundamental component of many modern software systems

---

## Key Concepts to Review

- [[SQL]]
- [[Redundant Data]]
- [[Normalization]]
- [[Entity]]
- [[Primary Key]]
- [[Foreign Key]]
- [[Null]]
- [[ACID Principles]]
- [[Atomicity]]
- [[Consistency]]
- [[Isolation]]
- [[Durability]]
- [[CRUD Applications]]
- [[Data Integrity]]
- [[Entity Integrity]]
- [[Domain Integrity]]
- [[Referential Integrity]]
- [[Relational Database]]
- [[Non-Relational Database]]
- [[NoSQL Database]]
- [[Horizontal Scalability]]
- [[Vertical Scaling]]
- [[Key-Value Stores]]
- [[Wide Column Stores]]
- [[Document Stores]]
- [[Graph Databases]]
- [[Search Databases]]
- [[RDBMS]]
- [[DBMS]]
- [[Schema]]
- [[Database Management Applications]]
- [[Multi-User Access]]
- [[API Server]]

### Database Systems

- [[PostgreSQL]]
- [[MySQL]]
- [[MariaDB]]
- [[MS SQL Server]]
- [[Oracle Database]]
- [[Microsoft Access]]
- [[H2 Database]]
- [[MS SQL Express]]
- [[SQLite]]
- [[DynamoDB]]
- [[Redis]]
- [[Apache Cassandra]]
- [[HBase]]
- [[Couchbase]]
- [[Firebase]]
- [[MongoDB]]
- [[Neo4j]]
- [[Elasticsearch]]
- [[Solr]]

### Management Tools

- [[DBeaver]]
- [[MySQL Workbench]]
- [[MS SQL Management Studio]]
- [[pgAdmin]]

---

## Review Questions

1. What are the three modification problems (anomalies) that occur in poorly designed single-table databases? Explain each with an example.
    
2. Define the following terms and explain how they work together:
    
    - Primary Key
    - Foreign Key
    - Referential Integrity
3. What is normalization, and why is it important in database design?
    
4. Explain the four ACID properties and why they matter for database reliability.
    
5. What are the three types of data integrity enforced by relational databases? Give an example of each.
    
6. Compare and contrast relational and non-relational databases. When would you choose one over the other?
    
7. What are the four main components of an RDBMS? Describe the purpose of each.
    
8. Explain the difference between a DBMS and a database management application. Provide examples.
    
9. In a dog-walking business database with three tables (Clients, Dogs, Walks), how would you structure the relationships using primary and foreign keys?
    
10. Describe two common database application architectures (e.g., web application architecture or enterprise application architecture) and explain how the components interact.
    
11. Why should you never manually edit database files directly? How should databases be accessed instead?
    
12. What does it mean for a database to support "multi-user access"? Why is this important in enterprise applications?
    
13. Give three examples of applications or systems you use daily that likely rely on databases. Explain what type of data they might store.
    
14. If you delete a row from the Walks table in a properly normalized database, why doesn't this affect the Clients or Dogs tables?
    
15. What is the difference between horizontal and vertical scalability? Which type of database typically uses each approach?
# Tags
#databases #data #computers #csd123 #saultcollege