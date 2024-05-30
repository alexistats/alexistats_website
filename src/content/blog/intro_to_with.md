---
title: "Quick Intro to SQL With Clause"
description: "Introducing SQL Common Expression Tables (CTE)"
pubDate: "February 22 2022"
heroImage: "/post_img.webp"
badge: "SQL"
tags: ["SQL", "CTE"]
---

Have you ever wondered how to make an SQL query more readable? Have you ever had to re-use the same sub-query in a join multiple time? Or perhaps, you just encountered “With” in an SQL query for the first time? Then read ahead to discover a whole new world of possibilities in SQL!

Defining the With Clause
Technically, “With” clauses are called “Common Table Expressions”, or CTE’s. I learned that the hard way, after failing to provide any sort of description for what a “CTE” is in an interview… only to discover that I used them all the time after googling the term!

With that out of the way, CTE’s are a powerful tool in SQL: They allow us to build entities that act as temporary tables within the query. Or, as reusable sub-queries within a complex query. It is even possible to use CTE’s in a recursive manner. CTE’s are similar to views, except that they are to be used for specific use-case (ie. inside a single query) instead of being available for general use.

Your SQL version’s documentation is probably the best place to look for understanding the specific syntax of a “With” clause, but in PostgreSQL, it is very simple to use, even with multiple CTE’s:

```
WITH
first_cte_name as (sql_query_here),
second_cte_name as (sql_query_here)
SELECT ... FROM ... 
```

The most basic way to build CTE’s is as above. Simply add the “With” clause to an SQL query, name the CTE followed by “as”, and write an SQL query between parentheses. Each definition is separated by a comma until the last definition. Then, write an SQL query as usual. The CTE’s can be used like any table would. They can be referenced in “FROM”, used in sub-queries, or joined, or vertically merged to existing tables in an SQL query.

Using CTE’s is not limited to a “SELECT” statement. It can be used with various statements such as SELECT INTO, CREATE TABLE AS, CREATE VIEW, DECLARE, EXPLAIN, INSERT INTO … SELECT, PREPARE, UPDATE, DELETE. See your documentation for the full list and special syntax that could apply.

---

### Common Table Expression Use-Cases

CTE’s are mainly used to improve readability and ease the maintenance of an SQL script since we are able to reuse them. In some cases, they can also significantly improve the performances of a complex query.

Another use-case worth mentioning are recursive CTE’s (yes, recursion in SQL!).

#### A use-case of a CTE

CTE’s can be of help by simply, improving the readability of SQL script. Take this example of a query with one join (using NHL data on player statistics and time on ice information):


![query_1.webp](/intro_to_with/query_1.webp)
It’s a simple query. There’s a sub-query in the FROM clause to calculate a bunch of different player statistics. Which is joined to another sub-query about icetime information.

Now, let’s take a look at the same query built using CTE’s.

![query_2.webp](/intro_to_with/query_2.webp)


The total number of lines is a little longer, but it is now much clearer what we are doing in the main query.

It already looks quite messy, but imagine if there were dozens of sub-queries? Or if we wanted to re-use a sub-query? In the case above, for sports data, a use case could be to extract a list of teams from a player’s stats table, and create queries for usage by team, offensive metrics by teams, etc. And at the end, join all those CTE’s under one readable, simpler query.

### Conclusion

To conclude, Common Table Expressions — the With clause — is a powerful and simple SQL clause that can be used with a multitude of statements to simplify and reuse sub-queries. They can be used to build more readable complex SQL statements by compartmentalizing sub-queries. And even, for the most curious and advanced users, CTE’s can be used for recursion in an SQL table.