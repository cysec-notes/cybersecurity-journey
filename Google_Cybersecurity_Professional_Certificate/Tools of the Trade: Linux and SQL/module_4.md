# Module 4:
## Overview
In this module, learners will learn how to use SQL to communicate with databases. They will learn how to query a database and filter the results. They will also learn how SQL can join multiple tables together in a query.

## Learning Objectives
After completing this module, I can:
- Discuss how SQL is used within the security profession.
- Describe how a relational database is organized.
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


## Skills Gained 
Using SQL commands to:
- select specific columns from a table,
- select all columns from a table by using an asterisk (*), and
- sort query results using the ORDER BY keyword.
- apply the WHERE clause to filter what a SQL query returns and
- use the LIKE operator to filter for patterns.
- Filter for login attempts made after a certain date
- apply AND, OR, and NOT operators to filter SQL queries.
## Personal Reflection




