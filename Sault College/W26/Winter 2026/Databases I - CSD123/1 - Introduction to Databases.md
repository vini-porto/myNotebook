# Database

A **[[database]]** is a structured collection of related data. Think of it as a highly efficient digital filing cabinet that lives on a computer. 

While you might use a spreadsheet like Excel for simple lists, databases are designed to handle massive amounts of data and allow you to find, update, or connect pieces of information almost instantly.

# Why Databases Matter

Databases are a core component of most modern information systems:

- **Web applications and websites** - storing user accounts, content, and settings

- **Mobile apps** - managing app data and user information

- **Desktop applications** - organising local data efficiently

- **Web browsers** - storing bookmarks, history, and cache

---

They provide a **robust way to store information** that is:

- **Fault tolerant** - can recover from crashes and errors
- **Data integrity enforcing** - ensures data follows rules and remains accurate
- **Powerful for analysis** - using query languages like [[SQL]]

# The Problem

## 1. The Updating Problem

**Problem**: What if Bob gets a new phone number?

When client information is repeated across multiple rows (because Bob has multiple dogs or multiple walks), you must update every single instance of Bob's phone number. This is:

- **Error prone** - you might miss some instances
- **Creates inconsistency** - if you miss some, you won't know which number is correct later

>[!NOTE] Root cause
>[[Redundant Data]] makes updates difficult and unreliable.

## 2. The Inserting Problem

**Problem**: How do you record information for clients whose dogs you haven't walked yet?

If you add just client information without walk data:

- You have **awkward blank cells**
- You must decide where to put these rows (beginning? end? mixed in?)
- Adding a second dog for an existing client requires **repeating all their contact information**

>[!NOTE] Root cause 
>Storing information about multiple entities (clients, dogs, walks) in a single table makes insertion awkward and redundant.

## 3. The Deleting Problem

**Problem**: What happens if you delete a row after realising the walk didn't actually happen?

When you delete the walk record:

- You **accidentally delete the client information** too
- Or you leave awkward empty cells if you only delete some fields

>[!NOTE] Root cause 
>Deleting rows from a table that stores multiple types of information can remove more data than intended.

# Multiple Tables

The answer to modification problems is **breaking data into multiple related tables**. This process is called [[Normalization]].

## Three-Table Structure

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

# Types of Databases

## Relational Databases (SQL)

![[Databases#Relational Databases]]

### Data Integrity in Relational Databases

Relational databases enforce three types of [[Data Integrity]]:

**[[Entity Integrity]]**: No primary key can be empty (null), ensuring every row is unique and identifiable.

**[[Domain Integrity]]**: Data must be the correct type—you can't put a name in a "Phone Number" column.

**[[Referential Integrity]]**: You cannot have a Foreign Key that points to a Primary Key that doesn't exist. This prevents "orphaned" data.

## Non-Relational Databases (NoSQL)

![[Databases#Non-Relational Databases]]

# Relational Database Management Systems 

![[RDBMS#What is RDBMS]]
## Components of an RDBMS

### 1. The Relational Database

The actual collection of related data files, consisting of:

- **[[Schema]]**: The structure or skeleton (table definitions, relationships, constraints)
- **Data**: The actual information stored in the tables

The database is usually stored as one or more files. **Important**: You should never manually edit these files always access them through the [[DBMS]].

### 2. Database Management System 

The [[DBMS]] is the system of programs that enables the management and execution of all aspects of an RDBMS. It's the "engine" that interprets and executes database commands.

**Server-based DBMS**: Consists of a server listening for [[SQL]] commands (e.g., [[PostgreSQL]] Server, [[MySQL Server]])

**File-based DBMS**: Usually consists of a single shell or code library that interprets SQL (e.g., [[SQLite]], [[H2 Database]])

### 3. Applications

Applications are programs used to interact with the database:

**[[Database Management Applications]]**: Used to create, analyze, and manage databases

- [[DBeaver]]
- [[MySQL Workbench]]
- [[MS SQL Management Studio]]
- [[pgAdmin]]

> [!NOTE] User Applications 
> Used by end-users to perform application-specific tasks, storing and retrieving data from the database. May communicate with multiple databases.

### 4. Users

Users interact with applications and have **permissions/roles** that govern how they may interact with the system. 

RDBMSs support **[[Multi-User Access]]**: many people can read and write to the database simultaneously without conflicts or data corruption.

# RDBMS vs DBMS

**DBMS** (Database Management System) is the software—the "engine."

**Database** is the actual collection of related data files.

**RDBMS** is a specific type of DBMS designed to manage relational data in tables.

**Important distinction**: A DBMS is NOT a database management application.

> [!NOTE] Example 
> 
> [[PostgreSQL]] is an RDBMS that consists of:
> 
> - **PostgreSQL Server** (the DBMS)
> - **[[pgAdmin]]** (a database management application for PostgreSQL)
> - **[[DBeaver]]** (a database management application that can connect to various DBMSs, including PostgreSQL)

# Common Database Application Architectures

## Desktop / Embedded Applications

In this architecture, the application and database run on the same machine:

- Application connects directly to a file-based DBMS
- Examples: [[Microsoft Access]], [[SQLite]], [[H2 Database]], [[MS SQL Express]]
- Common for single-user applications or small-scale systems

## Enterprise Applications

In this architecture, multiple applications connect to a centralized database server:

- Multiple users and applications access the same database simultaneously
- Server-based DBMS handles concurrent access
- Examples: [[MS SQL Server]], [[MySQL]], [[PostgreSQL]], [[Oracle Database]]
- Common for business applications with many users

## Web Applications

**Architecture**:

- **Front end**: Browser displays the user interface
- **Back end**: Server runs application logic
- **Database**: Stores application data

>Multiple browsers connect to the same server, which manages all database interactions.

## Mobile Applications

**Architecture**:

- **Front end**: Mobile app provides the user interface
- **[[API Server]]**: Handles requests from mobile apps
- **Database**: Stores application data

>Multiple mobile apps connect to an API server, which acts as an intermediary to the database.


# Review Questions

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