# What is RDBMS

**RDBMS** stands for **Relational Database Management System**. Its a software used to store data in tables and manage relationships between them.

---

- [[Database]] → a place to store data
- [[Management System]] → software that lets you create, read, update, and delete data
- [[Relational]] → data is organized in **tables that relate to each other**

# Relational Connection

You can connect tables using related keys. 

|id|name|
|---|---|
|1|Alice|
|2|Bob|

|id|user_id|product|
|---|---|---|
|1|1|Laptop|
|2|1|Mouse|
|3|2|Phone|

- `user_id` in **Orders** refers to `id` in **Users**
- This creates a **relationship** between tables

> This avoids data duplication and keeps data organized.

# Keys

**Primary Key:** Uniquely identifies a row in a table

**Foreign Key:** A column that references a primary key in another table

# Related Topics

- [[Database]]
- [[SQL]]
- [[Primary Key]]
- [[Foreign Key]]
- [[Schema]]
- [[Normalization]]
- [[Tables]]
- [[Query]]
- [[Data Types]]
- [[Transactions]]
- [[ACID Properties]]
- [[NoSQL]]
# Tags

#SQL #Database #RDBMS #Database #DataManagement #RelationalDatabase 