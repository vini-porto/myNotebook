## The Story So Far (Weeks 1-3)

### Week 1 (The Problem)

**Issue**: Spreadsheets are messy.

**Problem**: [[Redundancy]] leads to [[Anomalies]] (Update/Delete errors).

### Week 2 (The Tool)

**Learning**: We learned [[SQL]] (`SELECT`, `WHERE`) to talk to single tables.

### Week 3 (The Solution)

**Concept**: We learned the [[Relational Model]].

**Action**: We split data into separate tables (Minions, Bots) to fix the anomalies.

### Week 4 (The Challenge)

**New problem**: Now that the data is split apart... how do we glue it back together?

**Answer**: Enter the **[[JOIN]]**.

## Roadmap for Today

1. The Problem: Data is Split Up ([[Normalization]])
2. The Solution: The [[INNER JOIN]] (The Zipper)
3. Syntax Rules: [[Dot Notation]] & [[Aliasing]]
4. [[OUTER JOINS]]: Finding the Nulls
5. THE DANGER ZONE: [[Cross Joins]]
6. Advanced: [[Self Joins]] & [[Unions]]

## Context: The Factory Database

**Last week**: We Normalized our data.

**Structure**:

- Minions in a 'Minions' table
- Bots in a 'Bots' table

**Why?**: To avoid redundancy (Anomalies).

## The Problem

**Gru's request**: "I want a list of Minion Names and the Model Name of the robot they are building!"

**THE ISSUE**:

- 'Minion Name' is in Table A
- 'Model Name' is in Table B
- You cannot select from two tables at once... unless you **JOIN** them

**Challenge**: Data is spread across multiple tables by design (normalization), but we need to view it together.

## The Analogy: The Zipper

**Visualization**:

- **Table A** = Left side of a zipper
- **Table B** = Right side of a zipper
- **The JOIN** = The slider that locks them together row-by-row

**Matching mechanism**: Based on a matching tooth (The [[Foreign Key]]).

## 1. The INNER JOIN (The Standard)

**[[INNER JOIN]]**: Only return rows where there is a MATCH in BOTH tables.

### The Party Analogy

**Setup**:

- **Left Table**: People
- **Right Table**: Tickets
- **Inner Join**: Only people WITH tickets get in

**Result**: If someone doesn't have a ticket, they don't appear in the results.

## Visualizing Inner Join

**Tables**:

```
[Minions]           [Assignments]
Kevin (ID 2)  --->  (ID 2) Bot 500
Bob (ID 4)    --->  (ID 4) Bot 501
Jerry (ID 6)        (No Match)
```

**RESULT**: Kevin and Bob appear. Jerry is invisible (No assignment).

**Why Jerry is excluded**: No matching row in Assignments table.

## The JOIN Syntax

**Basic structure**:

```sql
SELECT * 
FROM Minions
JOIN Assignments ON Minions.MinionID = Assignments.MinionID;
```

**Key component**: The **[[ON Clause]]** tells the database how to match the rows.

## Example Code: Multi-Table Join

```sql
SELECT Minions.Name, Bots.ModelName
FROM Minions
JOIN Assignments ON Minions.MinionID = Assignments.MinionID
JOIN Bots ON Assignments.BotID = Bots.BotID;
```

**Flow**: Minions → Assignments → Bots

**Result**: Connects minion names with the bot models they're building.

## Rule #1: Disambiguation (Dot Notation)

**Problem**: Both tables have a column named 'ID'.

**Query attempt**:

```sql
SELECT ID FROM Minions JOIN Bots...
```

**Database Error**: "[[Ambiguous Column Name]] ID"

**The Fix**: Use the **[[Table Name Prefix]]**.

```sql
SELECT Minions.ID, Bots.ID ...
```

**Why necessary**: The database needs to know which table's ID you're referring to.

## Spot the Error

**Broken code**:

```sql
SELECT Name, ReportsToID
FROM Minions
JOIN Assignments ON MinionID = MinionID;
```

**What's wrong?**: `ON MinionID = MinionID` is confusing! The DB doesn't know which table's MinionID.

**FIX**:

```sql
ON Minions.MinionID = Assignments.MinionID
```

**Lesson**: Always specify the table name when joining, especially for columns with the same name.

## Rule #2: Table Aliases (Nicknames)

**Problem**: Typing 'Assignments.MinionID' is tiring.

**Solution**: Give tables short **[[Table Aliases]]**.

```sql
SELECT m.MinionID
FROM Minions AS m
JOIN Assignments AS a ON m.MinionID = a.MinionID;
```

**Important rule**: Once you give a nickname, you **MUST use it everywhere** in the query.

**Benefit**: Makes queries more readable and less repetitive.

## The USING Shortcut

**Condition**: If the column name is IDENTICAL in both tables (e.g., 'MinionID' and 'MinionID'), you can use a shortcut.

**Standard syntax**:

```sql
ON a.MinionID = b.MinionID
```

**[[USING Shortcut]]**:

```sql
USING (MinionID)
```

**Complete example**:

```sql
SELECT m.MinionID
FROM Minions AS m 
JOIN Assignments AS a USING (MinionID);
```

**Warning**: This only works if the names match **perfectly**!

## 2. The LEFT JOIN (The Inclusive One)

**Scenario**: Gru wants a list of ALL Minions, even the ones who are lazy and have NO assignment.

**INNER JOIN problem**: Hides the lazy Minions (no match = no result).

**[[LEFT JOIN]] solution**: Shows everyone from the LEFT table, even if the RIGHT table is empty.

**Characteristic**: Returns all rows from the left table, with NULL for unmatched right table columns.

## Visualizing Left Join

**Tables**:

```
[Minions]           [Assignments]
Kevin (ID 1)  --->  (ID 1) Bot 500
Bob (ID 2)    --->  (ID 2) Bot 501
Dave (ID 3)         NULL
```

**RESULT**: Kevin, Bob, AND Dave appear.

**Dave's data**: Dave has **NULL** for his assignment because no matching row exists.

## Power Move: Finding the Lazy Minions

**Use case**: LEFT JOIN can find missing data.

```sql
SELECT m.Name
FROM Minions m
LEFT JOIN Assignments a ON m.MinionID = a.MinionID
WHERE a.BotID IS NULL;
```

**Result**: This returns the lazy Minions (those without assignments).

**How it works**: The **[[IS NULL]]** filter finds rows where the join found no match (broken links).

**Pattern**: LEFT JOIN + WHERE IS NULL = find records in left table with no matching records in right table.

## 3. The RIGHT JOIN

**[[RIGHT JOIN]]**: The exact opposite of LEFT JOIN.

**Behavior**: Take everything from the RIGHT table, match to the Left.

**Reality Check**: Nobody uses this.

**Why?**: Because 'A RIGHT JOIN B' is exactly the same as 'B LEFT JOIN A'.

**Best practice**: Just flip the tables and stick to LEFT JOIN. It reads better (Left to Right).

## 4. The FULL OUTER JOIN

**[[FULL OUTER JOIN]]**: Give me EVERYTHING.

**Includes**:

- All Minions (even if no task)
- All Tasks (even if no Minion assigned)

**Database support**:

- **MySQL**: Does NOT support this! (You have to fake it with [[Unions]])
- **PostgreSQL**: Supports it fine

**Use case**: Find all unmatched records from both tables.

## Summary: The Party Analogy

**INNER JOIN**: Only people with Tickets enter.

**LEFT JOIN**: All People enter. If no ticket, they hold a blank sign ([[NULL]]).

**RIGHT JOIN**: All Tickets enter. If no person, the ticket floats in the air (NULL).

**FULL JOIN**: Everyone and Everything enters. Chaos.

## 5. The DANGER ZONE: Cross Joins

**[[CROSS JOIN]]**: The [[Cartesian Product]].

**Behavior**: Pairs EVERY row in Table A with EVERY row in Table B.

**Syntax**:

```sql
SELECT * FROM Minions, Bots;
```

**Notice**: There is NO 'ON' clause!

## The Explosion

**Scenario**:

- 10,000 Minions
- 50,000 Cookie Bots

**Result of Cross Join**: 10,000 × 50,000 = **500,000,000 rows**!

**Effect**: The server crashes. Dr. Nefario fires you.

**Danger**: This is almost never what you want and can bring down production systems.

## Spot the Error: Missing ON Clause

**Broken code**:

```sql
SELECT * FROM Minions JOIN Bots;
```

**What happens?**: If you forget the 'ON' clause, some databases default to a CROSS JOIN.

**Always**: Double check your 'ON' condition!

**Prevention**: Always include an ON clause with JOIN statements.

## Joining 3+ Tables

**Scenario**: Minion Name + Bot Model + Part Name.

**Path**: We need to jump from Minion → Assignment → Bot → Parts.

```sql
SELECT m.Name, p.PartName
FROM Minions m
JOIN Assignments a ON m.MinionID = a.MinionID
JOIN Bots b ON a.BotID = b.BotID
JOIN BillOfMaterials bom ON b.BotID = bom.BotID  -- Junction Table!
JOIN Parts p ON bom.PartID = p.PartID;
```

**Concept**: It's just a chain of zippers!

**Pattern**: Each JOIN connects to the previous result, building up the full dataset.

## 6. The Self Join

**Recall**: [[Recursive Relationships]] (The Org Chart).

**Scenario**: Minions have Bosses who are also Minions.

**Challenge**: We need to join the table TO ITSELF.

## Self Join Syntax

**Trick**: You must Alias the table **twice**.

```sql
SELECT 
    Worker.Name AS Minion_Name, 
    Boss.Name AS Boss_Name
FROM 
    Minions AS Worker
JOIN 
    Minions AS Boss 
ON Worker.ReportsToID = Boss.MinionID;
```

**Visualization**: Imagine cloning the table. One is the 'Worker' list, one is the 'Boss' list.

## Self Join – Code Walkthrough

### Step 1: FROM Minions AS Worker

**The Code**: We start by grabbing the Minions table.

**The Trick**: We give it a temporary nickname (Alias) called **Worker**.

**Think**: Imagine picking up a printed copy of the list and writing "Worker List" on top in Sharpie.

### Step 2: JOIN Minions AS Boss

**The Code**: We grab a second copy of that exact same Minions table.

**The Trick**: We give this second copy a different nickname: **Boss**.

**Think**: Imagine picking up a second printed copy of the same list and writing "Boss List" on top. Now you have two lists on your desk.

### Step 3: ON Worker.ReportsToID = Boss.MinionID

**The Code**: This is the zipper. We need to match rows.

**The Action**:

1. Look at a specific Worker (e.g., Kevin)
2. Check his ReportsToID (which is #1)
3. Go to the "Boss List" and find the person with MinionID #1 (which is Gru)

**The Result**: The database connects Kevin (from the Worker pile) to Gru (from the Boss pile).

### Step 4: SELECT Worker.Name AS Minion_Name, Boss.Name AS Boss_Name

**The Output**: Now that they are connected, we pick what we want to see.

**Worker.Name**: "Kevin" (The employee)

**Boss.Name**: "Gru" (The manager)

**[[AS Keyword]]**: We rename the columns so the report doesn't confusingly say "Name" and "Name".

### Summary of Self Join

**Concept**: A Self Join is just pretending one table is actually two different tables so you can compare them side-by-side.

**Key mechanism**: The alias (`AS`) is what makes the "pretending" possible.

## 7. Sets: The UNION

**Contrast**:

- **Joins**: Horizontal (Adding Columns)
- **[[UNION]]**: Vertical (Stacking Rows)

**Scenario**: A list of ALL Names (Minions AND Villains).

```sql
SELECT Name FROM Minions
UNION
SELECT Name FROM Villains;
```

**Result**: All names from both tables in a single column, with duplicates removed.

**[[UNION ALL]]**: Includes duplicates (not shown but available).

## Summary Checklist

1. **Inner Join**: Exact matches only
2. **Left Join**: Keep all left rows + matches
3. **Cross Join**: Cartesian Explosion (Avoid!)
4. **Disambiguate**: Always use `TableName.ColumnName`
5. **Alias**: Use short nicknames (`AS m`)

## Lab Prep: The Factory Report

**Lab 4 task**: Generate reports for Gru's Factory.

**You will need JOINs to answer**:

1. **"Who built the Mega-Cookie?"** (Inner Join: Minions → Assignments → Bots)
    
2. **"Which parts are just gathering dust?"** (Left Join: Parts → BillOfMaterials)
    
3. **"Who does Kevin report to?"** (Self Join: Minions → Minions)
    

**WARNING**: Beware the Cross Join explosion!

---

## Key Concepts to Review

### Foundational Concepts

- [[Redundancy]]
- [[Anomalies]]
- [[SQL]]
- [[Relational Model]]
- [[JOIN]]
- [[Normalization]]
- [[Foreign Key]]

### JOIN Types

- [[INNER JOIN]]
- [[LEFT JOIN]]
- [[RIGHT JOIN]]
- [[FULL OUTER JOIN]]
- [[CROSS JOIN]]
- [[OUTER JOINS]]
- [[Self Joins]]

### Syntax Elements

- [[ON Clause]]
- [[Dot Notation]]
- [[Aliasing]]
- [[Table Aliases]]
- [[Ambiguous Column Name]]
- [[Table Name Prefix]]
- [[USING Shortcut]]
- [[IS NULL]]
- [[AS Keyword]]

### Advanced Concepts

- [[Cartesian Product]]
- [[Recursive Relationships]]
- [[UNION]]
- [[UNION ALL]]
- [[NULL]]

---

## Review Questions

1. What were the problems with spreadsheets discussed in Week 1? What are anomalies?
    
2. In Week 3, we split data into separate tables. What problem does this create that JOINs solve?
    
3. Explain the "zipper" analogy for JOINs. What are the teeth of the zipper?
    
4. What is an INNER JOIN? Using the party analogy, who gets in?
    
5. Write the basic syntax for an INNER JOIN between Minions and Assignments tables.
    
6. What does the ON clause do in a JOIN statement?
    
7. What error occurs if you SELECT a column name that exists in multiple joined tables without specifying which table?
    
8. How do you fix an ambiguous column name error? What is "dot notation"?
    
9. What are table aliases? Why would you use them?
    
10. If you create an alias for a table using AS, can you still use the original table name in the rest of the query?
    
11. What is the USING shortcut? When can you use it? When can't you use it?
    
12. What is a LEFT JOIN? How is it different from an INNER JOIN?
    
13. Using the party analogy, explain who gets in with a LEFT JOIN.
    
14. Write a query using LEFT JOIN to find all Minions who have NO assignments.
    
15. What is a RIGHT JOIN? Why does the lecture say "nobody uses this"?
    
16. What is a FULL OUTER JOIN? Which database systems support it?
    
17. What is a CROSS JOIN? What is the Cartesian Product?
    
18. Calculate: If you CROSS JOIN a table with 1,000 rows and a table with 500 rows, how many rows result?
    
19. What happens if you forget the ON clause when writing a JOIN? Why is this dangerous?
    
20. How do you join more than 2 tables together? Write an example joining 3 tables.
    
21. What is a Self Join? When would you use one?
    
22. In a Self Join, why do you need to alias the same table twice?
    
23. Write a Self Join to show employees and their managers from a Minions table where ReportsToID points to another MinionID.
    
24. What is a UNION? How is it different from a JOIN?
    
25. Explain the difference between "horizontal" (JOINs) and "vertical" (UNIONs) data combination.
    
26. Given two tables - Students(StudentID, Name) and Courses(CourseID, CourseName) with an Enrollments table connecting them - write a query to show all student names and the courses they're enrolled in.
    
27. Write a LEFT JOIN to find all Students who are NOT enrolled in any courses.
    
28. Why is this query dangerous: `SELECT * FROM Products, Orders;`
    
29. What's wrong with this query and how do you fix it?
    
    ```sql
    SELECT Name, BotID
    FROM Minions
    JOIN Assignments ON MinionID = MinionID;
    ```
    
30. Create a query that joins 3 tables: Customers → Orders → Products to show customer names and the products they ordered.
    

---

## Practical Exercises

### Exercise 1: Basic INNER JOIN

Given:

- **Employees** table: EmployeeID, Name, DepartmentID
- **Departments** table: DepartmentID, DepartmentName

Write a query to show all employee names with their department names.

### Exercise 2: LEFT JOIN for Missing Data

Using the same tables, write a query to find all employees who are NOT assigned to any department.

### Exercise 3: Multi-Table JOIN

Given:

- **Authors** table: AuthorID, AuthorName
- **Books** table: BookID, Title, AuthorID
- **Sales** table: SaleID, BookID, Quantity

Write a query to show author names, book titles, and quantities sold.

### Exercise 4: Self Join

Given a table **Employees** (EmployeeID, Name, ManagerID) where ManagerID references EmployeeID:

Write a query to show each employee's name alongside their manager's name.

### Exercise 5: Find Orphaned Records

Given:

- **Products** table: ProductID, ProductName
- **OrderItems** table: OrderItemID, ProductID, Quantity

Write a query to find all products that have never been ordered.

### Exercise 6: Multiple JOINs

Given:

- **Students** table: StudentID, StudentName
- **Enrollments** table: EnrollmentID, StudentID, CourseID
- **Courses** table: CourseID, CourseName, InstructorID
- **Instructors** table: InstructorID, InstructorName

Write a query to show student names, course names, and instructor names for all enrollments.

### Exercise 7: UNION

Given:

- **CurrentEmployees** table: EmployeeID, Name
- **FormerEmployees** table: EmployeeID, Name

Write a query to create a list of all employee names (current and former).

### Exercise 8: Complex Self Join

Given an **OrgChart** table (EmployeeID, Name, ManagerID, Level):

Write a query to show three levels of hierarchy: employee, their manager, and their manager's manager.

### Exercise 9: Fix the Cross Join

This query is broken and will cause a Cartesian explosion:

```sql
SELECT *
FROM Customers, Orders;
```

Fix it to properly join customers with their orders using CustomerID.

### Exercise 10: Advanced Filtering with JOINs

Given:

- **Customers** table: CustomerID, Name, City
- **Orders** table: OrderID, CustomerID, OrderDate, Total

Write queries to: a) Find all customers from "Toronto" and their orders b) Find all customers from "Toronto" who have NEVER placed an order c) Find the total amount spent by each customer from "Toronto"

---

## Common Mistakes to Avoid

1. **Forgetting the ON clause** - Results in a CROSS JOIN (Cartesian explosion)
2. **Ambiguous column names** - Not using table.column notation when columns exist in multiple tables
3. **Using original table name after aliasing** - Once you alias, must use the alias everywhere
4. **Confusing LEFT JOIN with INNER JOIN** - LEFT keeps all left rows; INNER only keeps matches
5. **Using WHERE instead of ON** - ON is for join conditions; WHERE is for filtering results
6. **Not understanding NULL behavior** - LEFT JOIN creates NULLs for unmatched rows
7. **Forgetting to alias in Self Joins** - Must alias the table twice to differentiate
8. **Using USING when column names don't match** - USING only works with identical column names
9. **Circular join logic** - Creating joins that don't make logical sense (Minion joins to itself incorrectly)
10. **Not testing with small datasets** - Always test joins with limited data first to avoid performance issues
11. **Mixing up join order in multi-table joins** - Order matters for readability and understanding
12. **Using RIGHT JOIN** - Just flip the tables and use LEFT JOIN instead
13. **Not considering performance** - Joining large tables without proper indexes can be very slow
14. **Forgetting AS keyword for column aliases** - Good practice to use AS even though it's optional in some databases
15. **Not checking for NULL values after LEFT JOIN** - Need IS NULL, not = NULL

---

## Join Decision Flowchart

**Question 1**: Do you need all records from the left table regardless of matches?

- **YES** → Use LEFT JOIN
- **NO** → Continue to Question 2

**Question 2**: Do you only want records that have matches in both tables?

- **YES** → Use INNER JOIN
- **NO** → Continue to Question 3

**Question 3**: Are you joining a table to itself?

- **YES** → Use Self JOIN (with aliases)
- **NO** → Continue to Question 4

**Question 4**: Do you want every possible combination of rows?

- **YES** → Use CROSS JOIN (but are you SURE? This is usually a mistake!)
- **NO** → Go back and reconsider your requirements

---

## SQL Join Performance Tips

1. **Use proper indexes** - Ensure foreign key columns are indexed
2. **Select only needed columns** - Don't use SELECT * in production
3. **Filter early** - Apply WHERE conditions before joining when possible
4. **Use EXPLAIN** - Check query execution plans to understand performance
5. **Limit result sets** - Use LIMIT during testing to avoid processing millions of rows
6. **Consider join order** - Sometimes reordering joins improves performance
7. **Avoid CROSS JOINs** - Unless absolutely necessary for a specific purpose

---

## Practical Tags for Obsidian

#SQL #DatabaseJoins #InnerJoin #LeftJoin #SQLJoins #DatabaseDesign #Normalization #ForeignKeys #SQLSyntax #DatabaseQueries #RelationalDatabases #DataRetrieval #SQLAdvanced #SelfJoin #CrossJoin #OuterJoin #UnionSQL #SQLBestPractices #DatabaseOptimization #QueryWriting #SQLTutorial #DataManagement #DatabaseRelationships #JoinSyntax #SQLPerformance