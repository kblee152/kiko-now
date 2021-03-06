---
layout: post
title: "Intermediate SQL Subquery: WHERE are the Subqueires?"
tags: [Datacamp]
comments: true
---

Datacamp `Intermediate SQL` Chapter_2_Short-and-Simple-Subqueries   
WHERE are the Subqueries 요약

Subqueries are incredibly powerful for performing complex filters and transformations. You can filter data based on single, scalar values using a subquery in ways you cannot by using `WHERE` statements or joins. Subqueries can also be used for more advanced manipulation of your data set. You will likely encounter subqueries in any real-world setting that uses relational databases.

##### What is a subquery?
- A query nested inside another query

```sql
SELECT column
FROM (SELECT column
      FROM table) AS subquery;
```
- Useful for intermediary transformations

##### What do you do with subqueries?
- Can be in any part of a query(to use for filtering or joining)
  - `SELECT`, `FROM`, `WHERE`, `GROUP BY`
- Can return a variety of information
  - Scalar queantities (`3.14159`, `-2`, `0.001`)
  - A list(`id = (12, 25, 392, 401, 939)`)
  - A table

> Where you place it depends on what you want your final data to look like

##### Why subqueries?
- Comparing groups to summarized values
  - How did Liverpool compare to the English Premier League's average performance for that year?
- Reshaping data
  - What is the highest monthly average of goals scored in the Bundesliga?
- Combining data that cannot be joined
  - How do you get both the home and away team names into a table of match results?


##### Simple Subqueries
- Can be evaluated independently from the outer query

```sql
SELECT home_goal
FROM match
WHERE home_goal > (
    SELECT AVG(home_goal)
    FROM match);

SELECT AVG(home_goal) FROM match;
```

- Is only processed once in the entire statement

```sql
SELECT home_goal
FROM match
WHERE home_goal > (
    SELECT AVG(home_goal)
    FROM match);
```

The subquery in WHERE is processed first, generating the overall average of home goals scored.  
SQL then moves onto the main query, treating the subquery like the single, aggregate value it just generated.

##### Subqueries in the WHERE clause
- Which matches in the 2012/2013 season scored home goals higher than overall average?

```sql
SELECT AVG(home_goal) FROM match;
```
> 1.56091291478423 

calculate the average, and then include that number in the main query

```sql
SELECT date, hometeam_id, awayteam_id, home_goal, avway_goal
FROM match
WHERE season = '2012/2013'
    AND home_goal > 1.56091291478423;
```

Or put the query directly into the WHERE clause, inside parentheses

```sql
SELECT date, hometeam_id, awayteam_id, home_goal, away_goal
FROM match
WHERE season = '2012/2013'
    AND home_goal > (SELECT AVG(home_goal)
                    FROM match);
```

| date       | hometeam_id | awayteam_id | home_goal | away_goal |
|------------|-------------|-------------|-----------|-----------|
| 2012-07-28 | 9998        | 1773        | 5         | 2         |
| 2012-10-05 | 9993        | 9991        | 2         | 2         |


##### Subquery filtering list with IN
- Subquery are useful for generating a filtering list
- Which teams are part of Poland's league?

```sql
SELECT
    team_long_name,
    team_short_name AS abbr
FROM team
WHERE
    team_api-id IN
    (SELECT hometeam_id
    FROM match
    WHERE country_id = 15722);
```




##### Practice

```sql
SELECT
    team_long_name,
    team_short_name
FROM team
WHERE team_api_id NOT IN
    (SELECT DISTINCT hometeam_id FROM match);
```

To filtering using a single-value (scalar) subquery, you can create a list of values in a subquery to filter data based on a complex set of conditions. This type of subquery generates a one column reference list for the main query. As long as the values in your list match a column in your main query's table, you don't need to use a join -- even if the list is from a separate table.