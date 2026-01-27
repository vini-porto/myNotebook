# Talking to Your Data: SQL Basics

## Database Refresher: The "Filing Cabinet"

### The Dog Walking Business (Review)

Recall the dog-walking business from the previous lecture with clients Dave, Kevin, Stuart, and Bob.

**The Problem**: We normalized a messy spreadsheet into three well-structured tables to eliminate [[Modification Problems]].

**The Solution**: Three related tables:

- **Clients** (Who pays us)
- **Dogs** (Who we walk)
- **Walks** (When we work)

### The Database Structure (Schema)

**Clients Table**:

- ClientID ([[Primary Key]])
- Name
- Address

**Dogs Table**:

- DogID ([[Primary Key]])
- Name
- Breed
- ClientID ([[Foreign Key]] linking to Clients)

**Walks Table**:

- WalkID ([[Primary Key]])
- Date
- Duration
- DogID ([[Foreign Key]] linking to Dogs)

## Why Not Just Use Excel?

Databases offer significant advantages over spreadsheets:

### Scale

**Excel**: Crashes at approximately 1 million rows **Databases**: Handle billions of rows efficiently

### Concurrency

**Excel**: Only one person can edit at a time **Databases**: 1,000+ users can query simultaneously without conflicts (thanks to [[Multi-User Access]])

### Security

**Excel**: Difficult to control who sees what data **Databases**: Fine-grained [[Access Control]]—you can prevent Bob from seeing Dave's credit card information

## What is SQL?

**[[SQL]]** (Structured Query Language) is a standard programming language used to interact with and manage data stored in [[Relational Databases]].

**Purpose**: Universal language for database operations, enabling users to:

- **Store** data
- **Retrieve** data
- **Update** data
- **Delete** data

All operations use simple, English-like commands.

### SQL is Declarative

**[[Declarative Programming]]**: You describe **what** you want, not **how** to get it.

**Analogy**:

- **[[Procedural Programming]]** (Python/Java): "Walk to the kitchen, open fridge, get milk."
- **Declarative** (SQL): "Bring me milk."

The database engine figures out the most efficient way to retrieve your data.

### RDBMS Examples

SQL works across multiple **[[RDBMS]]** platforms:

**[[MySQL]] / [[MariaDB]]**: Popular for web applications, open-source, widely used

**[[PostgreSQL]]**: Advanced, feature-rich, open-source (commonly used in CSD courses)

**[[SQL Server]]**: Microsoft's enterprise database solution

**[[Oracle Database]]**: Corporate heavyweight for large enterprises

**Important note**: The SQL we learn works on almost ALL of these platforms with minimal differences.

### How Relational Databases Work

**[[Relational Databases]]** organize data into **tables** consisting of:

- **Rows** (records) - individual data entries
- **Columns** (fields) - attributes or properties

These tables can be **linked together** through defined relationships using [[Primary Keys]] and [[Foreign Keys]], ensuring [[Data Integrity]] and consistency.

## The Anatomy of a SQL Query

### The Basic Command Structure

The "Big Three" [[SQL Clauses]]:

1. **[[SELECT Clause]]**: Which columns do you want?
2. **[[FROM Clause]]**: Which table contains the data?
3. **[[WHERE Clause]]**: Which rows meet your conditions?

### The Mental Model: Order of Execution

**Crucial Concept**: You write SELECT first, but the computer executes FROM first.

**[[SQL Execution Order]]**:

1. **Find the Table** (FROM) - Locate the data source
2. **Filter Rows** (WHERE) - Apply conditions to select specific rows
3. **Return Columns** (SELECT) - Choose which columns to display

Understanding this order helps you write better queries and debug problems.

## SQL Formatting Rules (Style Guide)

Following consistent formatting makes SQL readable and maintainable:

### Keywords

**Style**: Write in UPPERCASE **Examples**: `SELECT`, `FROM`, `WHERE`, `ORDER BY`

### Table and Column Names

**Conventions**:

- **[[PascalCase]]**: First letter of every word capitalized, no spaces (e.g., `ClientName`, `OrderHistory`, `FirstName`)
- **[[snake_case]]**: Words separated by underscores, lowercase (e.g., `client_name`, `order_history`, `first_name`)

**Standard practice**: `snake_case` is generally preferred for SQL table and column names (e.g., `user_id` instead of `UserId`), while PascalCase is often used in application code.

### Newlines and Structure

**Best practice**: Every clause gets its own line for readability.

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### The Terminator: Semicolon

**[[Semicolon]]** (`;`): Marks the end of a SQL statement. Required to execute the command.

## SQL Comments

**[[SQL Comments]]** allow you to leave notes for other developers (or your future self):

**Single-line comment**:

```sql
-- This is a comment
SELECT * FROM Dogs; -- Gets all dogs
```

**Block comment**:

```sql
/* This is a 
   multi-line comment
   spanning several lines */
```

## Selecting Data: Basic Queries

### Hello World: Select All

**The [[Wildcard Asterisk]]** (`*`): Selects all columns.

```sql
SELECT * FROM Dogs;
```

**Result**: Shows all columns—DogID, Name, Breed, ClientID

**Warning**: Never use `SELECT *` in production applications—it returns too much data and impacts performance. Always specify only the columns you need.

### Selecting Specific Columns

**Best practice**: Specify exactly which columns you need.

```sql
SELECT DogName, Breed FROM Dogs;
```

**Benefits**:

- Reduces data transfer
- Improves query performance
- Makes code more maintainable

## Column Aliases (AS)

**[[Column Alias]]**: Rename columns in the output to make them more readable.

**Syntax**: Use the `AS` keyword

```sql
SELECT DogName, Breed AS Type FROM Dogs;
```

**Result**: The `Breed` column appears as `Type` in the output.

**Use case**: Making reports friendlier for non-technical stakeholders—they see "Type" instead of "Breed."

## String Concatenation

**[[String Concatenation]]**: Combining multiple columns into one.

**Operator**: `||` (double pipe)

```sql
SELECT ClientName || ' lives at ' || Address AS Summary
FROM Clients;
```

**Result**: "Dave lives at 22 Beagle Crescent"

**Use case**: Creating formatted messages or labels from multiple database fields.

**Note**: Some databases use different operators (`+` in SQL Server, `CONCAT()` function in MySQL).

## The WHERE Clause: Filtering Data

The **[[WHERE Clause]]** is the filter mechanism of SQL.

**Purpose**: Without it, you get every row in the table. With it, you get only rows that meet your conditions.

**Syntax**:

```sql
SELECT * FROM table_name WHERE condition;
```

### Filtering Numbers

**No quotes needed** for integers or decimals.

```sql
SELECT * FROM Walks WHERE Duration > 30;
```

**[[Comparison Operators]]**:

- `=` Equal to
- `>` Greater than
- `<` Less than
- `>=` Greater than or equal to
- `<=` Less than or equal to
- `<>` or `!=` Not equal to

### Filtering Text

**Rule**: Text MUST be enclosed in **single quotes** (`'`).

```sql
SELECT * FROM Clients WHERE ClientName = 'Bob';
```

**Common error**:

```sql
WHERE ClientName = Bob  -- WRONG! Database looks for a column named Bob
```

Always use quotes around text values.

### Filtering Dates

**Rule**: Dates are treated as strings in SQL queries.

**Standard format**: `'YYYY-MM-DD'`

```sql
SELECT * FROM Walks WHERE WalkDate = '2025-12-25';
```

**Note**: Date formats may vary by database system, but ISO format (YYYY-MM-DD) is universally supported.

## Logical Operators

### The AND Operator

**[[AND Operator]]**: Both conditions must be true.

**Scenario**: Find long walks taken by specific dogs.

```sql
SELECT * FROM Walks 
WHERE Duration > 30 AND DogID = 1;
```

**Logic**: Returns rows where BOTH duration exceeds 30 AND the dog's ID is 1.

### The OR Operator

**[[OR Operator]]**: At least one condition must be true.

**Scenario**: Find walks that were either very short or very long.

```sql
SELECT * FROM Walks 
WHERE Duration < 15 OR Duration > 60;
```

**Logic**: Returns rows where EITHER duration is less than 15 OR greater than 60.

### The NOT Operator

**[[NOT Operator]]**: Exclude specific data (negation).

```sql
SELECT * FROM Clients WHERE NOT ClientName = 'Dave';
```

**Alternate syntax**:

```sql
WHERE ClientName != 'Dave';
WHERE ClientName <> 'Dave';
```

All three versions exclude records where ClientName is 'Dave'.

### Order of Operations (Logic)

**Problem**: Mixing AND/OR without parentheses creates ambiguity.

**Rule**: `AND` has higher precedence (processed first) than `OR`.

**Solution**: Always use **[[Parentheses]]** when mixing logical operators.

**Example**:

```sql
SELECT * FROM Clients
WHERE (ClientName = 'Bob' OR ClientName = 'Kevin') 
  AND City = 'Sault Ste. Marie';
```

Without parentheses, the logic may execute differently than intended.

## Advanced Filtering Operators

### The IN Operator

**[[IN Operator]]**: A shortcut for multiple OR statements.

```sql
SELECT * FROM Dogs 
WHERE Breed IN ('Beagle', 'Poodle', 'Pug');
```

**Equivalent to**:

```sql
WHERE Breed = 'Beagle' OR Breed = 'Poodle' OR Breed = 'Pug';
```

**Benefit**: More concise and readable, especially with many values.

### The BETWEEN Operator

**[[BETWEEN Operator]]**: Selecting a range (inclusive of both endpoints).

```sql
SELECT * FROM Walks 
WHERE WalkDate BETWEEN '2025-12-20' AND '2025-12-31';
```

**Logic**: Returns walks from December 20 through December 31 (both dates included).

**Works with**: Numbers, dates, and sometimes text (alphabetical ranges).

## Pattern Matching with LIKE

**[[LIKE Operator]]**: Used when you only know part of the text you're searching for.

### The Percent Wildcard (%)

**[[Percent Wildcard]]** (`%`): Represents zero, one, or many characters.

```sql
SELECT * FROM Clients 
WHERE Address LIKE '%Crescent%';
```

**Matches**: "22 Beagle Crescent", "15 Oak Crescent Drive", "Crescent View"

**Common patterns**:

- `'A%'` - Starts with A
- `'%Z'` - Ends with Z
- `'%text%'` - Contains "text" anywhere

### The Underscore Wildcard (_)

**[[Underscore Wildcard]]** (`_`): Represents exactly one character.

```sql
SELECT * FROM Clients 
WHERE Phone LIKE '415-___-____';
```

**Matches**: Any phone number in the 415 area code (e.g., "415-123-4567")

**Use case**: When you know the exact length but not all characters.

### Case Sensitivity

**Important note**: `LIKE` is often case-insensitive, but this depends on the database configuration.

**PostgreSQL specific**: Use **[[ILIKE]]** for guaranteed case-insensitive matching.

```sql
-- PostgreSQL
WHERE Name ILIKE 'bob%'; -- Matches "Bob", "bob", "BOB", "Bobby"
```

## Handling NULL Values

### What is NULL?

**[[NULL]]** is a special value in SQL:

- **NOT zero** (`0`)
- **NOT an empty string** (`''`)
- **Means**: "Unknown" or "Missing"

**Concept**: NULL represents the absence of a value.

### IS NULL

**Problem**: You cannot use `=` with NULL.

```sql
WHERE Email = NULL  -- WRONG! This never works
```

**Correct syntax**: Use **[[IS NULL]]**

```sql
SELECT * FROM Clients WHERE Email IS NULL;
```

**Returns**: All clients without an email address on file.

### IS NOT NULL

**Scenario**: Get a list of clients who definitely have phone numbers.

```sql
SELECT * FROM Clients WHERE Phone IS NOT NULL;
```

**Returns**: All clients with a phone number (excluding missing/unknown values).

## Sorting Results: ORDER BY

### The ORDER BY Clause

**[[ORDER BY Clause]]**: Sorts query results.

**Important concept**: Databases store data in random/optimized order, not in any logical sequence. You must explicitly request sorting.

**Placement**: Comes AFTER the WHERE clause.

**Syntax**:

```sql
SELECT columns FROM table WHERE conditions ORDER BY column;
```

### Ascending Sort (ASC)

**[[ASC]]** (Ascending): Default sort order.

**Order**:

- Text: A-Z
- Numbers: 0-9
- Dates: Oldest-Newest

```sql
SELECT * FROM Dogs ORDER BY DogName ASC;
```

**Note**: `ASC` is optional—if you omit it, ascending is assumed.

### Descending Sort (DESC)

**[[DESC]]** (Descending): Reverse order.

**Order**:

- Text: Z-A
- Numbers: 9-0
- Dates: Newest-Oldest

```sql
SELECT * FROM Walks ORDER BY WalkDate DESC;
```

**Use case**: Show recent walks first.

### Sorting by Multiple Columns

**Scenario**: Sort by one column, then by another within each group.

```sql
SELECT * FROM Players 
ORDER BY Team ASC, LastName ASC;
```

**Logic**: First sorts by Team alphabetically, then within each team, sorts players by LastName.

## Limiting Results

### LIMIT / TOP

**[[LIMIT Clause]]**: Restricts the number of rows returned.

**Syntax varies by database**:

**MySQL/PostgreSQL**:

```sql
SELECT * FROM Dogs LIMIT 5;
```

**SQL Server**:

```sql
SELECT TOP 5 * FROM Dogs;
```

**Use case**: "Just show me the first 5 results."

### Pagination with OFFSET

**[[OFFSET]]**: Skip a specified number of rows.

**Scenario**: Show rows 11-20 (page 2 of results).

```sql
SELECT * FROM Dogs 
LIMIT 10 OFFSET 10;
```

**Logic**:

- Skip first 10 rows (`OFFSET 10`)
- Return next 10 rows (`LIMIT 10`)

**Use case**: Implementing pagination in web applications—each page shows 10 results.

## Bringing It All Together: Complex Queries

### Mega Query Example

```sql
SELECT Name, Breed
FROM Dogs
WHERE Breed <> 'Poodle'
ORDER BY Name ASC
LIMIT 3;
```

**Breakdown**:

1. Select Name and Breed columns
2. From the Dogs table
3. Exclude Poodles (not equal to 'Poodle')
4. Sort alphabetically by Name
5. Show only the first 3 results

## Removing Duplicates: DISTINCT

**[[DISTINCT Keyword]]**: Eliminates duplicate values from results.

**Problem**:

```sql
SELECT Team FROM Players;
```

Returns "Sharks" 10 times (once for each player on the Sharks).

**Solution**:

```sql
SELECT DISTINCT Team FROM Players;
```

Returns "Sharks" only once, along with other unique team names.

**Use case**: Finding unique values—all cities where we have customers, all product categories, etc.

## Performing Calculations

### Math in the SELECT Clause

**Concept**: You can perform mathematical operations directly in the SELECT clause.

```sql
SELECT Duration, Duration * 60 AS DurationSeconds
FROM Walks;
```

**Result**: Shows original duration (in minutes) alongside calculated duration in seconds.

**Supported operations**:

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)

## Conditional Logic: CASE

**[[CASE Expression]]**: Like an IF statement inside SQL.

**Syntax**:

```sql
SELECT Name,
  CASE
    WHEN Breed = 'Poodle' THEN 'High Maintenance'
    ELSE 'Low Maintenance'
  END AS MaintenanceLevel
FROM Dogs;
```

**Logic**: For each row, evaluate conditions and return corresponding values.

**Result**: Each dog gets labeled as "High Maintenance" or "Low Maintenance" based on breed.

**Use cases**:

- Categorizing data
- Creating custom labels
- Conditional calculations

## Common Pitfalls

### Forgetting the Semicolon

**Problem**: Query doesn't execute.

**Solution**: Always end SQL statements with `;`

### Misspelling Column Names

**Problem**: Confusing data with schema.

**Example error**:

```sql
SELECT Naem FROM Dogs;  -- "Naem" doesn't exist
```

**Solution**: Double-check column names in your schema/documentation.

### Confusing = with LIKE

**Wrong**:

```sql
WHERE Name = 'B%';  -- Looks for exact match "B%"
```

**Correct**:

```sql
WHERE Name LIKE 'B%';  -- Finds names starting with B
```

## Debugging Broken Queries

### Error: Missing Quotes

**Problem**:

```sql
SELECT * FROM Dogs WHERE Breed = Beagle;
```

**Issue**: Database looks for a column named "Beagle" instead of the text value "Beagle".

**Fix**:

```sql
SELECT * FROM Dogs WHERE Breed = 'Beagle';
```

### Error: Wrong Clause Order

**Problem**:

```sql
SELECT * FROM Dogs
ORDER BY DogName ASC
WHERE Breed = 'Beagle';
```

**Issue**: Syntax error—WHERE must come before ORDER BY.

**Correct order**:

```sql
SELECT * FROM Dogs
WHERE Breed = 'Beagle'
ORDER BY DogName ASC;
```

**Remember**: [[SQL Clause Order]]:

1. SELECT
2. FROM
3. WHERE
4. ORDER BY
5. LIMIT

### Error: Logic Problem (The Greedy Query)

**Scenario**: Find walks that Kevin did that were short (< 15 mins).

**Problem**:

```sql
SELECT * FROM Walks
WHERE Walker = 'Kevin' OR Duration < 15;
```

**Issue**: Returns hundreds of rows—all of Kevin's walks (regardless of duration) AND all short walks (regardless of walker).

**Fix**: Use AND instead of OR

```sql
SELECT * FROM Walks
WHERE Walker = 'Kevin' AND Duration < 15;
```

**Lesson**: Be careful with OR—it's very inclusive. Use AND when both conditions must be true.

---

## Key Concepts to Review

### Database Fundamentals

- [[Modification Problems]]
- [[Primary Key]]
- [[Foreign Key]]
- [[Multi-User Access]]
- [[Access Control]]
- [[Data Integrity]]

### SQL Basics

- [[SQL]]
- [[Relational Databases]]
- [[RDBMS]]
- [[Declarative Programming]]
- [[Procedural Programming]]

### Database Systems

- [[MySQL]]
- [[MariaDB]]
- [[PostgreSQL]]
- [[SQL Server]]
- [[Oracle Database]]

### SQL Components

- [[SQL Clauses]]
- [[SELECT Clause]]
- [[FROM Clause]]
- [[WHERE Clause]]
- [[ORDER BY Clause]]
- [[LIMIT Clause]]
- [[SQL Execution Order]]
- [[SQL Clause Order]]

### Formatting and Style

- [[PascalCase]]
- [[snake_case]]
- [[Semicolon]]
- [[SQL Comments]]
- [[Wildcard Asterisk]]

### Query Operations

- [[Column Alias]]
- [[String Concatenation]]
- [[Comparison Operators]]
- [[AND Operator]]
- [[OR Operator]]
- [[NOT Operator]]
- [[Parentheses]]
- [[IN Operator]]
- [[BETWEEN Operator]]

### Pattern Matching

- [[LIKE Operator]]
- [[Percent Wildcard]]
- [[Underscore Wildcard]]
- [[ILIKE]]

### Special Values and Functions

- [[NULL]]
- [[IS NULL]]
- [[DISTINCT Keyword]]
- [[CASE Expression]]

### Sorting and Limiting

- [[ASC]]
- [[DESC]]
- [[OFFSET]]

---

## Review Questions

1. What are the three main advantages of using databases over Excel spreadsheets? Explain each with a specific example.
    
2. Explain the difference between declarative programming (SQL) and procedural programming (Python/Java). Use the "milk" analogy from the lecture.
    
3. What are the "Big Three" SQL clauses? What does each one do?
    
4. Describe the mental model of SQL execution order. Why is it important to understand that you write SELECT first but the computer executes FROM first?
    
5. What is the difference between PascalCase and snake_case? Which is generally preferred for SQL table and column names?
    
6. Why should you never use `SELECT *` in production applications? What should you do instead?
    
7. Write a SQL query that selects the Name and Breed columns from the Dogs table. Add a column alias so that Breed appears as "Type" in the output.
    
8. What is string concatenation? Write a query that combines FirstName and LastName into a single column called FullName from a Clients table.
    
9. Explain the difference between filtering numbers and filtering text in SQL. What's the common error people make with text filters?
    
10. What are the six comparison operators available in SQL? Provide an example query using at least three of them.
    
11. Explain the difference between AND and OR operators. Create a scenario where using OR instead of AND produces incorrect results.
    
12. What is the IN operator and why is it useful? Rewrite this query without using IN:
    
    ```sql
    SELECT * FROM Dogs WHERE Breed IN ('Beagle', 'Poodle', 'Pug');
    ```
    
13. What is the BETWEEN operator? Write a query that finds all walks that occurred in December 2025.
    
14. Explain the difference between the `%` wildcard and the `_` wildcard in LIKE queries. Give an example of when you'd use each.
    
15. What is NULL in SQL? Why doesn't `WHERE Email = NULL` work? What's the correct syntax?
    
16. What does the ORDER BY clause do? What's the default sort order if you don't specify ASC or DESC?
    
17. Write a query that selects all dogs, sorted first by Breed (ascending) and then by Name (descending) within each breed.
    
18. What's the difference between LIMIT in MySQL/PostgreSQL and TOP in SQL Server? Write equivalent queries for both that return the first 10 rows.
    
19. Explain how OFFSET works for pagination. Write a query that displays rows 21-30 from the Walks table.
    
20. What does the DISTINCT keyword do? When would you use it? Provide a practical example.
    
21. Write a query using the CASE expression that categorizes dogs by size:
    
    - Breed is 'Chihuahua' or 'Pug' → 'Small'
    - Breed is 'Beagle' → 'Medium'
    - All others → 'Large'
22. Fix this broken query and explain what was wrong:
    
    ```sql
    SELECT * FROM Dogs WHERE Breed = Beagle;
    ```
    
23. Fix this broken query and explain the error:
    
    ```sql
    SELECT * FROM Dogs
    ORDER BY Name ASC
    WHERE Breed = 'Poodle';
    ```
    
24. Explain the logic problem in this "greedy query" and fix it:
    
    ```sql
    SELECT * FROM Walks
    WHERE Walker = 'Kevin' OR Duration < 15;
    ```
    
    (Goal: Find Kevin's short walks only)
    
25. Write a complete query that:
    
    - Selects DogName and Breed from Dogs table
    - Excludes Poodles
    - Only shows dogs whose names start with 'B'
    - Sorts by DogName alphabetically
    - Limits results to 5 rows

---

## Practice Exercises

### Exercise 1: Basic Selection

Write queries for a Clients table with columns: ClientID, ClientName, City, Phone, Email

a) Select all clients from 'Toronto' b) Select ClientName and Phone for clients whose email is not NULL c) Select all columns for clients whose names start with 'S'

### Exercise 2: Filtering with Multiple Conditions

Using a Walks table with columns: WalkID, DogID, WalkDate, Duration, Walker

a) Find walks longer than 45 minutes that occurred in January 2025 b) Find walks by either 'Kevin' or 'Stuart' that lasted less than 20 minutes c) Find walks between December 20-31, 2025, excluding walks by 'Bob'

### Exercise 3: Pattern Matching

Using a Dogs table with columns: DogID, DogName, Breed, ClientID

a) Find dogs whose names end with 'y' b) Find dogs whose breed contains the word 'Terrier' c) Find dogs with exactly 4-letter names (use underscore wildcard)

### Exercise 4: Sorting and Limiting

Using a Products table with columns: ProductID, ProductName, Category, Price

a) Show the 10 most expensive products b) Show products sorted by Category (ascending), then Price (descending) c) Show products 11-20 when sorted by ProductName (pagination)

### Exercise 5: Complex Query

Write a single query that:

- Uses the Walks table
- Finds walks between 30-60 minutes (inclusive)
- Excludes walks by 'Bob'
- Orders by WalkDate (newest first)
- Shows only the first 15 results
- Includes a calculated column showing duration in hours (Duration / 60) with alias 'DurationHours'

---

## Pop Quiz Answers

**Question**: What does this return?

```sql
SELECT * FROM Dogs WHERE DogName LIKE 'B%';
```

**Answer**: All dogs whose names start with the letter 'B' (e.g., Bello, Bobby, Buddy, Bruno).

---

## Practical Tips

### Writing Readable Queries

1. **Use uppercase for keywords**: `SELECT`, `FROM`, `WHERE`
2. **Put each major clause on a new line**
3. **Indent conditions** under WHERE for readability
4. **Use meaningful aliases**: `AS CustomerName` not `AS CN`
5. **Add comments** to explain complex logic

### Common Gotchas to Avoid

1. **Forgetting quotes around text values**: `WHERE City = Toronto` (wrong)
2. **Using = with NULL**: `WHERE Email = NULL` (wrong, use `IS NULL`)
3. **Wrong clause order**: WHERE must come before ORDER BY
4. **Mixing AND/OR without parentheses**: Always use parentheses for clarity
5. **Case sensitivity in LIKE**: Use ILIKE in PostgreSQL for case-insensitive matching

---

## SQL Clause Execution Order Summary

**Writing Order** (how you type it):

1. SELECT
2. FROM
3. WHERE
4. ORDER BY
5. LIMIT

**Execution Order** (how the database processes it):

1. FROM (find the table)
2. WHERE (filter rows)
3. SELECT (choose columns)
4. ORDER BY (sort results)
5. LIMIT (restrict number of rows)

Understanding this difference helps you write better queries and understand why certain queries work or fail.

---

## Practical Tags for Obsidian

#SQL #Database #RDBMS #QueryLanguage #DataRetrieval #PostgreSQL #MySQL #SQLServer #DataFiltering #DatabaseDesign #SQLBasics #DataManagement #SQLSyntax #DatabaseQuerying #DataAnalysis #CRUD #RelationalDatabase #SQLTutorial #LearnSQL #DatabaseProgramming