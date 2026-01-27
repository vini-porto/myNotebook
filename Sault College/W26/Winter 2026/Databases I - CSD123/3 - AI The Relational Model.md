# Roadmap for Today

Today's journey takes us from messy data to well-structured blueprints:

1. SQL Review (The "How" from last week)
2. What is a "Relation"? (The Definition)
3. Keys: PK + FK (The "ID Cards")
4. Integrity Rules (The "Laws")
5. Relationships & Cardinality (The "Family Tree")

**Journey**: We are going from Messy → Rules → Blueprints

## Week 1 Review: Why Lists Fail

### Data vs. Information

**[[Data]]**: Raw facts (e.g., "Banana")

**[[Information]]**: Data with meaning (e.g., "We are out of Bananas")

### The Problem with Lists and Excel: The Three Anomalies

**[[Update Anomaly]]**: When you change data in one place but forget other instances.

**Example**: You change "Gru" to "Dru" in one row but forget the other 99 rows. Now you have inconsistent data.

**[[Insert Anomaly]]**: When you can't add new data without having related data first.

**Example**: You can't add a new Minion until they are assigned a job. (Bad design!)

**[[Delete Anomaly]]**: When deleting data accidentally removes other important information.

**Example**: You delete the "Arctic Mission" and accidentally delete all the Minions who were on it. (Data Loss!)

**The Fix**: The **[[Relational Database]]** (what we're building today).

## Week 2 Review: The Mental Model

### SQL Execution Order

Remember: You WRITE `SELECT` first, but the computer READS `FROM` first.

**[[SQL Execution Order]]**:

1. **FROM**: Pick the Table (The Jar)
2. **WHERE**: Filter the Rows (Red marbles only)
3. **SELECT**: Pick the Columns (Show me the size)

### The 'Quote' Trap

**Common error**: `SELECT * FROM Dogs WHERE Breed = Beagle;`

**Why it fails**: Text must be in quotes.

**The Fix**:

- **Numbers** (50, 3.14) are naked → `WHERE Duration > 15`
- **Text** ('Dave') gets dressed in quotes → `WHERE Walker = 'Dave'`

**Correct**: `SELECT * FROM Dogs WHERE Breed = 'Beagle';`

### Logic Check: AND vs. OR

**Scenario**: Find Kevin's SHORT walks (< 15 mins).

**Wrong**: `WHERE Walker = 'Kevin' OR Duration < 15`

- **Result**: All of Kevin's walks + EVERY short walk by Bob

**Correct**: `WHERE Walker = 'Kevin' AND Duration < 15`

**Rule**:

- **[[AND Operator]]** restricts (narrows results)
- **[[OR Operator]]** expands (widens results)

### The 'Ghost' Column Error

**Error**: `no such column 'Name'`

**Why?**: In the lab database, the column is named `ClientName` or `DogName`.

**Lesson**: The database is literal—it cannot guess what you mean. Always check how your table is constructed!

## Introduction to The Relational Model

### History and Concept

**[[Relational Model]]**: Invented by **[[E.F. Codd]]** (IBM) in 1970.

**Core concept**: Data is stored in **[[Relations]]** (tables).

**Why important?**: Before this, databases were messy hierarchies. This brought math and logic to data storage.

## Is it a Table or a Relation?

**Important distinction**: Not all tables are Relations.

**[[Relation]]**: A table that follows three strict rules:

### Rule 1: Unique Rows

**[[Unique Rows Rule]]**: No two rows can be identical.

**Why?**: If you have two identical "Dave" rows, how do you delete just one of them?

**Solution**: This is why we need **[[Primary Keys]]** (IDs).

### Rule 2: Atomic Cells

**[[Atomic Cells Rule]]**: Each cell must contain a single, indivisible value.

**Violation example**: Gru writes "Beagle, Pug" in one cell to save space.

**Problem**: This is **[[Multi-Valued Attribute]]**.

**Why it breaks SQL**: `WHERE Breed = 'Beagle'` will fail.

**The Fix**: One cell, one value. Split it into new rows.

### Rule 3: Order Doesn't Matter

**[[Order Irrelevance Rule]]**: Row order is meaningless in a database.

**Contrast with Excel**: In Excel, Row 1 is "First." In a database, Row 1 is just "A Row."

**Analogy**: A bag of Scrabble tiles. There is no "first" tile until you pull one out.

**Application**: If you want order, you MUST use `ORDER BY`.

```sql
SELECT *
FROM Walks
ORDER BY WalkDate DESC, Duration ASC;
```

## Terminology Check: The Fancy Words

**Important for exams**:

|Common Term|Academic Term|
|---|---|
|Table|[[Relation]]|
|Row|[[Tuple]] (pronounced "TOO-pull")|
|Column|[[Attribute]]|

**Note**: We'll say Table/Row/Column in class, but you must know the academic terms for exams!

## What is a Key?

**[[Key]]**: One or more columns used to identify a row.

**The Problem**: How do we tell "Kevin the Minion" apart from "Kevin the Accountant"?

**Solution**: We need a unique identifier.

## Candidate Keys

**[[Candidate Key]]**: Any column (or combination of columns) that COULD successfully identify a unique record.

**Minion Example**:

- FingerprintID (Unique? **Yes**)
- EmailAddress (Unique? **Yes**)
- GoggleSize (Unique? **No** - Many share sizes)

**Result**: Fingerprint and Email are both Candidate Keys.

## The Primary Key

**[[Primary Key]]** (PK): The Candidate Key we choose to use as the main identifier.

### Selection Criteria

**Short**: Numbers are better than long emails

**Never Changes**: People change emails; they don't change IDs

**Never Null**: Must always exist

**Purpose**: The "chosen one" among candidate keys.

## Surrogate Keys

**[[Surrogate Key]]**: An artificial identifier created just for database purposes.

**Scenario**: Our dogs don't have Social Insurance Numbers.

**Solution**: We invent one! `DogID`

**Definition**: A meaningless number generated by the database (1, 2, 3...) just to be unique.

**Pros**:

- Simple
- Fast
- Never changes

## Natural Keys

**[[Natural Key]]**: Data that already exists in the real world and is unique.

**Examples**:

- SIN (Social Insurance Number)
- VIN (Vehicle Identification Number) on a car
- ISBN on a book

**Cons**:

- Real-world data is sometimes messy
- Privacy laws may prevent using it
- Can change over time

## Composite Keys

**[[Composite Key]]**: When ONE column isn't enough, we use TWO (or more) together.

**Example**: Student_Grades Table

**Individual attempts fail**:

- StudentID? (No—student takes 5 classes)
- CourseID? (No—30 students in the class)

**Solution**: StudentID + CourseID? **YES**

- Dave's Student ID in CSD123 happens only once

**Result**: The combination is unique even though individual parts aren't.

## The Foreign Key

**[[Foreign Key]]** (FK): A column that points to the Primary Key of ANOTHER table.

**Example**: `Dogs.OwnerID` points to `Clients.ClientID`

**Role**: This is the glue that makes the database "Relational." It connects the data.

**Purpose**: Establishes relationships between tables.

## The Three Laws of Data Integrity

**[[Data Integrity]]**: Three fundamental rules ensuring data quality:

1. **[[Entity Integrity]]** (Identity)
2. **[[Domain Integrity]]** (Type)
3. **[[Referential Integrity]]** (Relationships)

## Law #1: Entity Integrity

**[[Entity Integrity Rule]]**: The Primary Key cannot be NULL.

**Translation**: "Every row must have a name tag."

**Why?**: If a row has no ID, the database can't:

- Find it
- Update it
- Delete it

**Result without ID**: It becomes a **[[Ghost Row]]**—unusable and unreachable.

## Law #2: Domain Integrity

**[[Domain Integrity Rule]]**: Data must match the column constraints.

**Translation**: "No square pegs in round holes."

**Examples**:

- Phone column cannot hold "Twenty"
- Age column cannot hold "-5"
- Color column must be from the list ['Red', 'Blue']

**Purpose**: Ensures data types and constraints are respected.

## Law #3: Referential Integrity

**[[Referential Integrity Rule]]**: If you point to a record (via Foreign Key), it must exist.

**Translation**: "No Dead Ends."

**Scenario**: You cannot add a Dog with `OwnerID = 99` if Client #99 doesn't exist.

**Purpose**: This prevents **[[Orphaned Records]]**—child records without parents.

**Critical importance**: This is "The Big One"—the most important integrity constraint.

## Handling Deletions: Cascade Options

**Problem**: What if we delete Client #1 (Dave)?

### Option A: Restrict

**[[ON DELETE RESTRICT]]**: Database says "NO! Dave owns dogs. Delete the dogs first."

**Characteristic**: Safest option—prevents accidental data loss.

### Option B: Cascade

**[[ON DELETE CASCADE]]**: Database deletes Dave AND automatically deletes all his dogs.

**Characteristic**: Dangerous! Can cause unintended data loss.

### Option C: Set Null

**[[ON DELETE SET NULL]]**: Dave is gone; the dogs' `OwnerID` becomes NULL.

**Result**: "Stray dogs"—orphaned records with no parent reference.

## Pop Quiz: Name the Violation

### Question 1

**Q**: I try to enter "Bob" into the Price column?

**A**: **Domain Integrity** violation

**Why**: Domain Integrity enforces the type of data allowed in a column. A "Price" column is defined as numeric (money) domain. "Bob" is text, not a number.

### Question 2

**Q**: I try to add a Walk for Dog #500, but we only have 5 dogs?

**A**: **Referential Integrity** violation

**Why**: Referential Integrity protects relationships between tables. You cannot enter a Foreign Key (Dog #500) in the child table if that Primary Key doesn't exist in the parent "Dogs" table. You can't walk a dog that doesn't exist!

### Question 3

**Q**: I try to create a new Client without an ID?

**A**: **Entity Integrity** violation

**Why**: Entity Integrity ensures every row is uniquely identifiable. This rule states that a Primary Key can never be NULL. Without an ID, the database cannot distinguish this client from any other.

## What is Cardinality?

**[[Cardinality]]**: "How many of THAT relate to how many of THIS?"

**Simple definition**: Cardinality is just a fancy word for "The Count."

### Two Types of Cardinality

**[[Maximum Cardinality]]** (The limit):

- **Question**: "Can a Customer have Many orders, or just One?"

**[[Minimum Cardinality]]** (Optionality):

- **Question**: "Does a Customer have to have an order to exist, or can they have Zero?"

**Purpose**: When you draw a line between two tables (like Customers and Orders), Cardinality defines the numeric rules of that relationship.

## The 'Thousand Minion' Problem

**Scenario**: Gru has a contract to build 50,000 Spy Cookie-Bots.

### Tracking Requirements

**1. The Workforce**:

- 10,000 Minions (Names, IDs, Fingerprints)
- Certifications (Food Safe vs. Welding)
- Payroll (Bananas per hour, Bonuses)
- Equipment (Goggles, Overalls, Gloves)
- Medical (Eye exams, Mutation history)
- Cafeteria (Dietary restrictions, Lunch shifts)
- Housing (Bunk assignments, Nightlights)

**2. The Factory** (Mixed Inventory):

- Hardware: Microchips, Wheels, Lenses
- Bakery: Flour, Chocolate Chips, Sprinkles
- Assembly: Which chip goes in which cookie?

### The Reality

**Problem**: You cannot track this in your head. Did Kevin eat the guidance chip?

**Critical lesson**: "You cannot code this from memory. You cannot use a spreadsheet. If you build a skyscraper without a blueprint, it falls down. If you build a database without an **[[ERD]]** (Entity Relationship Diagram), it crashes."

## The Symbols: Crow's Foot Notation

**[[Crow's Foot Notation]]**: Standard symbols for drawing ER Diagrams.

**Basic symbols**:

- **One Line (|)**: "One"
- **[[Crow's Foot]] (<)**: "Many"
- **Circle (O)**: "Optional" (Zero)

**Purpose**: Visual language for database design.

## Mandatory vs. Optional Relationships

**[[Mandatory One]] (||)**: Must have exactly one.

- **Example**: Every Person has a Mother

**[[Optional One]] (O|)**: Can have zero or one.

- **Example**: A Person might have a Spouse, or not

**[[Mandatory Many]] (|<)**: Must have at least one.

- **Example**: An Order must have at least one Product

**[[Optional Many]] (O<)**: Can have zero to many.

- **Example**: A Client might have 0 Dogs, or 10 Dogs

## Relationship Types: 1:N (One-to-Many)

**[[One-to-Many Relationship]]**: The standard relationship—90% of your design.

**Example**: One employee can place zero or many supply orders.

**Rule**: The Foreign Key always goes on the "Many" side.

- Supply Orders table holds the `EmployeeID`

**Most common**: This is the foundational relationship pattern.

## Relationship Types: M:N (Many-to-Many)

**[[Many-to-Many Relationship]]**: The "Problem Child" of database design.

### Example: Students and Classes

**Fact A**: One Student (Bob) can register for Many Classes (Databases, Networking, Programming)

**Fact B**: One Class (CSD123) can have Many Students (Bob, Dave, Kevin)

### The Problem

**If you put ClassID in Student table**: Bob can only take one class

**If you put StudentID in Class table**: The class can only have one student

**Neither works**: A database cell can only hold one value, not a list

**Physical Reality**: You CANNOT build this directly in a database.

**Solution**: The **[[Junction Table]]**.

## The Junction Table (The Fix)

**[[Junction Table]]**: A middleman table that breaks M:N into two 1:N relationships.

**Example**: `Student_Classes` Table

**Visual Check**: The Crow's Feet point IN toward the new middle table.

**Mnemonic**: "The Junction Table is the center of attention."

### Many-to-Many Analogy: Minions and Bosses

**Fact A**: One Minion (Kevin) serves Many Bosses over his life (T-Rex, Napoleon, Gru)

**Fact B**: One Boss (Gru) has Many Minions (Kevin, Stuart, Bob, Dave...)

### Why the Database "Brain" Breaks

**The Gru Problem**: If you try to write the names of all Gru's minions on his single ID card, you'll run out of ink. No room for 10,000 names on one card.

**The Kevin Problem**: If you look at Kevin's ID card, you can't list every boss he's ever served. Too messy.

**The Rule**: You physically cannot draw a direct line between them. A database cell can only hold one thing, not a list.

**Solution**: Create a third thing—A Clipboard (The Junction Table). This clipboard has no brain; it just records relationships.

## Relationship Types: 1:1 (One-to-One)

**[[One-to-One Relationship]]**: The rare case.

**Example**: Minion and Heart (One Minion has one Heart)

**Design**: Usually, just merge them into one table.

### Exception: Security

**Use case for 1:1**: Separating sensitive data.

**Left Table (Employees)**: Safe, boring data (Name, Phone)

- Receptionist or IT Helpdesk can see this

**Right Table (Employee_Salaries)**: Dangerous data (Money, Banking Info)

- Only Payroll Manager has access

**Purpose**: Regular staff don't need to know how many bananas Kevin is making.

## Identifying Relationship

**[[Identifying Relationship]]**: The "Clingy" Child relationship.

**Definition**: The Child table CANNOT exist without the Parent.

**Technical Rule**: The Foreign Key is part of the Child's Primary Key.

**Visual notation**: Drawn as a **SOLID Line**.

**Example**: OrderLineItems cannot exist without an Order.

## Non-Identifying Relationship

**[[Non-Identifying Relationship]]**: The Independent Child.

**Definition**: The Child is related to the Parent but can exist on its own.

**Technical Rule**: The Foreign Key is just a normal column (not part of the PK).

**Visual notation**: Drawn as a **DOTTED Line**.

**Example**: An Order belongs to a Customer, but Orders has its own ID independent of the Customer.

## Let's Diagram the Lab! (Part 1)

### Clients and Dogs

**Relationship**: 1:N (One-to-Many)

**Constraint 1**: A Dog must have an Owner (**Mandatory** on Dog side)

**Constraint 2**: An Owner might not have a dog yet (**Optional** on Client side)

**Foreign Key**: `OwnerID` in Dogs table points to `ClientID` in Clients table

## Let's Diagram the Lab! (Part 2)

### Dogs and Walks

**Relationship**: 1:N (One-to-Many)

**Logic**: One Dog goes on Many Walks

**Foreign Key**: `DogID` is inside the Walks table

## Handling the 'Multi-Dog Walk'

**Question**: What if Kevin walks 3 dogs at once?

**Current Lab Design**: Can't handle it well!

- Row 1: Kevin-DogA
- Row 2: Kevin-DogB
- Problem: Duplicates walk information

**Better Design**: We need an M:N Junction Table (`Walk_Participants`)

**When we'll learn this**: Advanced Design module

## Supertype & Subtype (Inheritance)

**[[Supertype-Subtype Relationship]]**: Database inheritance pattern.

### Scenario: Cookie-Bot Mixed Parts

**Problem**: Microchips have Voltage; Dough has Expiration Date

**If we put them in one table**: "Dough" has an empty Voltage column (NULL). Messy!

### The Solution: Divide and Conquer

**1. [[Supertype]]** (Parent): `Parts` (ID, Name, Cost)

- Common attributes all parts share

**2. [[Subtype]]** (Children):

- `Hardware` (Voltage)
- `Food` (Expiry)

**Rule**: Is it a Part? Yes. What KIND? Hardware.

## Recursive Relationships (Self-Referencing)

**[[Recursive Relationship]]**: When a table points to itself.

### Scenario: The Minion Org Chart

**Hierarchy**:

- Kevin reports to Stuart
- Stuart reports to Gru

**Question**: Do we create a "Bosses" table?

**Answer**: NO! Bosses are Minions too.

### The Solution

**Table**: Minions

**Columns**:

- `MinionID` (PK)
- `Name`
- `ReportsToMinionID` (FK)

**Key characteristic**: The Foreign Key matches a Primary Key in the SAME table.

## Summary of Rules

**Relations**: Unique Rows, Atomic Cells, Order Irrelevance

**Keys**:

- PK (Identity)
- FK (Link between tables)
- Composite (Combination)

**Integrity**:

- Entity (No Ghosts—PK can't be NULL)
- Referential (No Orphans—FK must point to existing PK)
- Domain (No Errors—data must match type constraints)

## Coming Up Next Week

**Topic 1: Normalization**

- How to take a messy spreadsheet and apply these rules to "clean" it

**Topic 2: JOINS**

- Learn the SQL to connect tables (INNER JOIN)

## Lab 3 Preview

**Topic**: Drawing Diagrams (ERDs)

**Tools**: Draw.io, Lucid.app, Visio (or paper)

**Goal**: Draw the Minion business correctly using the symbols we just learned

---

## Key Concepts to Review

### Data Quality Issues

- [[Data]]
- [[Information]]
- [[Update Anomaly]]
- [[Insert Anomaly]]
- [[Delete Anomaly]]
- [[Relational Database]]

### SQL Fundamentals

- [[SQL Execution Order]]
- [[AND Operator]]
- [[OR Operator]]

### Relational Model Foundations

- [[Relational Model]]
- [[E.F. Codd]]
- [[Relations]]
- [[Unique Rows Rule]]
- [[Atomic Cells Rule]]
- [[Multi-Valued Attribute]]
- [[Order Irrelevance Rule]]

### Academic Terminology

- [[Tuple]]
- [[Attribute]]

### Keys

- [[Key]]
- [[Candidate Key]]
- [[Primary Key]]
- [[Surrogate Key]]
- [[Natural Key]]
- [[Composite Key]]
- [[Foreign Key]]

### Integrity Constraints

- [[Data Integrity]]
- [[Entity Integrity]]
- [[Ghost Row]]
- [[Domain Integrity]]
- [[Referential Integrity]]
- [[Orphaned Records]]
- [[ON DELETE RESTRICT]]
- [[ON DELETE CASCADE]]
- [[ON DELETE SET NULL]]

### Relationships

- [[Cardinality]]
- [[Maximum Cardinality]]
- [[Minimum Cardinality]]
- [[ERD]]
- [[Crow's Foot Notation]]
- [[Crow's Foot]]
- [[Mandatory One]]
- [[Optional One]]
- [[Mandatory Many]]
- [[Optional Many]]

### Relationship Types

- [[One-to-Many Relationship]]
- [[Many-to-Many Relationship]]
- [[Junction Table]]
- [[One-to-One Relationship]]
- [[Identifying Relationship]]
- [[Non-Identifying Relationship]]
- [[Supertype-Subtype Relationship]]
- [[Supertype]]
- [[Subtype]]
- [[Recursive Relationship]]

---

## Review Questions

1. What are the three modification anomalies that occur in poorly designed databases? Give an example of each.
    
2. What is the correct execution order for SQL statements? Why is it different from the order you write them?
    
3. Explain the "quote trap." When do you use quotes in SQL WHERE clauses and when don't you?
    
4. What's the difference between using AND vs. OR in a WHERE clause? Provide an example where using OR gives unexpected results.
    
5. What is the Relational Model and who invented it? Why was it revolutionary?
    
6. What are the three rules that make a table a "relation"? Explain each with an example.
    
7. What is a "tuple" in database terminology? What about an "attribute"?
    
8. Define what a key is in a database. Why do we need keys?
    
9. What is a Candidate Key? If a table has multiple candidate keys, how do you choose which becomes the Primary Key?
    
10. Explain the difference between a Surrogate Key and a Natural Key. Give advantages and disadvantages of each.
    
11. What is a Composite Key? Provide a scenario where you would need to use one.
    
12. What is a Foreign Key? What role does it play in making a database "relational"?
    
13. Explain the three laws of data integrity: Entity, Domain, and Referential. Give an example of a violation for each.
    
14. What is the difference between ON DELETE RESTRICT, ON DELETE CASCADE, and ON DELETE SET NULL? Which is safest?
    
15. Identify the integrity violation: You try to insert a Walk record for DogID = 999, but only 10 dogs exist in the Dogs table.
    
16. What is cardinality in database relationships? Explain Maximum Cardinality vs. Minimum Cardinality.
    
17. Draw or describe the Crow's Foot notation symbols for: One, Many, Optional (Zero).
    
18. What's the difference between Mandatory One (||) and Optional One (O|)? Give a real-world example of each.
    
19. What is a One-to-Many relationship? Why is the Foreign Key always on the "Many" side?
    
20. What is a Many-to-Many relationship? Why can't you implement it directly in a database?
    
21. What is a Junction Table? How does it solve the Many-to-Many problem?
    
22. Using the Minions and Bosses analogy, explain why Many-to-Many relationships need a Junction Table.
    
23. What is a One-to-One relationship? When would you use it instead of just merging the tables?
    
24. Explain the security use case for One-to-One relationships using the Employees and Salaries example.
    
25. What's the difference between an Identifying Relationship and a Non-Identifying Relationship? How are they drawn differently?
    
26. What is a Supertype-Subtype relationship? Provide the Cookie-Bot parts example explaining why you'd use this pattern.
    
27. What is a Recursive Relationship (self-referencing)? Use the Minion org chart as an example.
    
28. In the Clients-Dogs relationship: Which side is mandatory and which is optional? Where does the Foreign Key go?
    
29. Why can't the current lab design handle Kevin walking 3 dogs at once? What structure would you need?
    
30. What is an ERD and why is it compared to a blueprint for a skyscraper?
    

---

## Practical Exercises

### Exercise 1: Identify the Anomaly

For each scenario, identify whether it's an Update, Insert, or Delete Anomaly:

a) You have a spreadsheet with student information repeated for each course they take. You update one student's phone number but miss other rows. The student now has 3 different phone numbers in the system.

b) You want to add a new course to your system, but you can't until at least one student enrolls in it.

c) A student drops their only course. When you delete that row, you lose all information about the student, including their contact information.

### Exercise 2: Relation Rules Violations

Identify which rule of relations is violated in each case:

a) A table with two identical rows: both say "Dave, 555-1234, Beagle"

b) A cell in the "Phone" column contains "555-1234, 555-5678, 555-9999"

c) You assume the first row in your table is the "oldest" customer

### Exercise 3: Integrity Violations

Identify which type of integrity is violated (Entity, Domain, or Referential):

a) A row in the Customers table has CustomerID = NULL

b) The Age column contains the value "Twenty-Five"

c) A row in Orders table has CustomerID = 500, but there's no customer with ID 500

d) A Price column contains -50.00

e) A row in the Products table has ProductID = NULL

### Exercise 4: Design the Relationship

For each scenario, determine:

- The type of relationship (1:1, 1:N, or M:N)
- Which table(s) should contain foreign key(s)
- Whether you need a junction table

Scenarios: a) Authors and Books (an author can write multiple books; a book can have multiple authors)

b) Countries and Capitals (each country has exactly one capital; each capital belongs to exactly one country)

c) Departments and Employees (each employee works in one department; each department has many employees)

d) Students and Courses (students take many courses; courses have many students)

e) Persons and Passports (each person has at most one passport; each passport belongs to exactly one person)

### Exercise 5: Draw the ERD

Using Crow's Foot notation, draw ERDs for:

a) **Library System**:

- Books (can be checked out multiple times over time)
- Members (can check out multiple books)
- CheckOuts (tracks which member has which book when)

b) **Hospital System**:

- Patients (can have multiple appointments)
- Doctors (can see multiple patients)
- Appointments (connects patients and doctors at specific times)

c) **Restaurant System**:

- Customers (place orders)
- Orders (contain multiple items)
- MenuItems (can appear in multiple orders)

### Exercise 6: Junction Table Creation

The scenario: Teachers and Subjects in a school.

- One teacher can teach many subjects
- One subject can be taught by many teachers

Create three tables showing:

1. Teachers table structure (columns)
2. Subjects table structure (columns)
3. Junction table structure (columns and foreign keys)

### Exercise 7: Cascade Options

For a database with Customers and Orders, explain what happens in each scenario:

a) Customer Dave (CustomerID = 5) has 3 orders. You try to delete Customer Dave.

- What happens with ON DELETE RESTRICT?
- What happens with ON DELETE CASCADE?
- What happens with ON DELETE SET NULL?

b) Which option is safest? Which is most dangerous? Why?

### Exercise 8: Identify Key Types

For a Students table, classify each as Surrogate, Natural, or Composite:

a) StudentNumber (auto-incrementing: 1, 2, 3...) b) SocialInsuranceNumber c) Combination of LastName + DateOfBirth d) EmailAddress e) DatabaseGeneratedGUID

### Exercise 9: Supertype-Subtype Design

Design a Supertype-Subtype structure for Vehicles:

- All vehicles have: VehicleID, Make, Model, Year
- Cars have: NumDoors, TrunkSize
- Motorcycles have: EngineCC, HasSidecar
- Trucks have: BedLength, TowingCapacity

Show the table structures.

### Exercise 10: Recursive Relationship

Design a table for representing an employee organizational hierarchy where:

- Every employee has an EmployeeID
- Every employee (except the CEO) reports to another employee
- You need to track: EmployeeID, Name, Title, ReportsTo

Show the table structure and explain how the recursive relationship works.

---

## Common Mistakes to Avoid

1. **Confusing candidate keys with primary keys** - All primary keys are candidate keys, but not all candidate keys become primary keys
2. **Putting foreign keys on the wrong side** - FK always goes on the "many" side of 1:N
3. **Trying to implement M:N directly** - Always need a junction table
4. **Forgetting entity integrity** - Primary keys can NEVER be NULL
5. **Mixing multiple values in one cell** - Violates atomic cells rule
6. **Assuming row order matters** - It doesn't! Use ORDER BY
7. **Creating orphaned records** - Always maintain referential integrity
8. **Using ON DELETE CASCADE without thinking** - Can accidentally delete massive amounts of data
9. **Overusing 1:1 relationships** - Usually better to merge tables unless security/performance reasons
10. **Not understanding the difference between identifying and non-identifying relationships** - Affects primary key composition
11. **Forgetting quotes around text in SQL** - Numbers naked, text dressed
12. **Using OR when you meant AND** - OR expands, AND restricts
13. **Creating junction tables with meaningful names** - Call it "StudentCourses" not "Enrollment"
14. **Not checking column names** - Database won't guess "Name" vs "ClientName"
15. **Relying on Excel habits in databases** - Order, duplicate rows don't work the same

---

## ERD Practice Scenarios

Create ERDs (Entity Relationship Diagrams) for:

### Scenario 1: University System

- Students enroll in many courses
- Courses have many students
- Each course has one instructor
- Instructors teach many courses
- Students have one major department
- Departments have many students

### Scenario 2: E-commerce Platform

- Customers place many orders
- Orders contain many products
- Products can be in many orders
- Each order has one shipping address
- Products belong to one category
- Categories contain many products

### Scenario 3: Movie Rental System

- Customers can rent many movies
- Movies can be rented by many customers (over time)
- Each rental has a due date and return date
- Movies belong to one or more genres
- Customers have one membership type

---

## Practical Tags for Obsidian

#Database #RelationalModel #DatabaseDesign #SQL #DataIntegrity #ERD #PrimaryKey #ForeignKey #Normalization #Cardinality #DatabaseRelationships #OneToMany #ManyToMany #JunctionTable #CrowsFootNotation #EntityIntegrity #ReferentialIntegrity #DomainIntegrity #DatabaseTheory #DataModeling #DatabaseKeys #CompositeKey #SurrogateKey #NaturalKey #DatabaseAnomalies #SQLFundamentals #DatabaseConstraints #ERDiagrams #RecursiveRelationship #SupertypeSubtype