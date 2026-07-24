# Module 4:
## Overview
In this module, learners will learn how to use SQL to communicate with databases. They will learn how to query a database and filter the results. They will also learn how SQL can join multiple tables together in a query.

## Learning Objectives
After completing this module, I can:
- Discuss how SQL is used within the security profession.
- Describe how a **relational database** is organized.
- Use SQL to retrieve information from a database.
- Apply filters to SQL queries.
- Use SQL joins to combine multiple tables into a query.

## Key Concepts Learned
#### What is Database?
**Database** as an organized collection of information or data. A relational database is a structured database containing tables that are related to each other.

The **primary key** refers to a column where every row has a unique entry. Unique and no duplicate
The **foreign key** is a column in a table that is a primary key in another table. can have duplicate

#### What is SQL (tructured Query Language.)
**SQL** is a programming language used to create, interact with, and request information from a database. A **query** is a request for data from a database table or a combination of tables. A **log** is a record of events that occur within an organization's systems. There are two essential keywords in any SQL query: SELECT and FROM.

#### Basic queries
**SELECT** indicates which columns to return. SELECT *  instructs SQL to return all columns from the specified table.

**FROM** indicates which table to query.

**WHERE** indicates the condition for a filter.

**LIKE** is an operator used with WHERE to search for a pattern in a column. for example; 

```text
WHERE username LIKE 'a%';
```

contains the correct syntax to return all records that contain a value in the username column that starts with the character 'a'. The LIKE operator is used with WHERE to search for a pattern in a column. The % wildcard substitutes for any number of other characters.

**Syntax** refers to the rules that determine what is correctly structured in a computing language.

**ORDER BY** sequences the records returned by a query based on a specified column or columns. This can be in either ascending or descending order.
1. Sorting in ascending order
  example:

```text
SELECT customerid, city, country
FROM customers
ORDER BY city;
```

2. Sorting in descending order

```text
SELECT customerid, city, country
FROM customers
ORDER BY city DESC;
```

3. Sorting based on multiple columns

 ```text
SELECT customerid, city, country
FROM customers
ORDER BY country, city;
```
#### Basic filters on SQL queries
**Filtering** is selecting data that match a certain condition.
An **operator** is a symbol or keyword that represents an operation.


#### Filter dates and numbers
Common Data types
1. string - is data consisting of an ordered sequence of characters. for example: user names, such as a user name: analyst10.
2. numeric - is data consisting of numbers, such as a count of log-in attempts.
3. date and time - data refers to data representing a date and/or time

**Date and Time operators:** =, <, >, <>, >=, <=

**BETWEEN** is an operator that filters for numbers or dates within a range.
Note: The BETWEEN operator is inclusive.

#### Filters with AND, OR, and NOT
1. **AND** is an operator that specifies that both conditions must be met simultaneously.
2. The **OR** operator is an operator that specifies that either condition can be met.
3. **NOT** negates a condition.
4. To find records where a column is **NULL** in SQL, use the **IS NULL** operator in your WHERE clause.
```text
SELECT patch_id, patch_applied_date, system_id 
FROM system_patches 
LEFT JOIN system ON system_patches.system_id = system.system_id 
WHERE patch_id IS NULL OR (patch_id = 'CRITICAL_PATCH_XYZ' AND patch_applied_date > '2023-10-26';
```

### Join tables in SQL
1. **INNER JOIN** returns rows matching on a specified column that exists in more than one table.

**Types of Outer Joints**
**Outer joins** also return rows that don't match on the specified column.

1. LEFT JOIN - returns all of the records of the first table, but only returns rows of the second table that match on a specified column.
2. RIGHT JOIN - returns all of the records of the second table but only returns rows from the first table that match on a specified column.
3. FULL OUTER JOIN - returns all records from both tables.

Example:
- INNER JOIN:
```text
SELECT machines.device_id, employees.username, machines.operating_system
FROM machines
INNER JOIN  employees ON machines.device_id = employees.device_id;
```

### Aggregate functions
In SQL, aggregate functions are functions that perform a calculation over multiple data points and return the result of the calculation. The actual data is not returned. 

There are various aggregate functions that perform different calculations:

1. **COUNT** returns a single number that represents the number of rows returned from your query.
Ex: SELECT COUNT(firstname) FROM customers;
AVG returns a single number that represents the average of the numerical data in a column.

SUM returns a single number that represents the sum of the numerical data in a column. 

## Skills Gained 
Using SQL commands to:
- select specific columns from a table,
- select all columns from a table by using an asterisk (*), and
- sort query results using the ORDER BY keyword.
- apply the WHERE clause to filter what a SQL query returns and
- use the LIKE operator to filter for patterns.
- Filter for login attempts made after a certain date
- apply AND, OR, and NOT operators to filter SQL queries.
- have practical experience in using INNER JOIN, LEFT JOIN, and RIGHT JOIN.

## Explore SQL applications in security
During the session covering SQL's role in security and relational database organization, focused on:
- Identifying where security-related data is stored.
- Connecting SQL to various security tasks.
- Applying SQL to specific security scenarios like investigating failed logins and missing patches.
- Exploring broader uses of SQL in cybersecurity.

My strengths:
- I demonstrated a clear understanding of how SQL queries can be constructed to extract specific information for security investigations.
- I effectively connected SQL's capabilities to practical cybersecurity tasks and scenarios.

Areas for improvement:
- Paying close attention to the precise syntax and logical structure of complex SQL queries, especially when combining multiple conditions or using LEFT JOIN with NULL checks, to ensure they accurately capture the intended data.





## Personal Reflection




