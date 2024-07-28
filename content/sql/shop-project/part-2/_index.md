---
content_type: project
flavours:
- none
learning_outcomes:
- sql_docker_composition
- sql_one_to_one_relationship
- sql_one_to_many_relationship
- sql_many_to_many_relation
prerequisites:
  hard:
  - projects/sql/shop-project/part-1
  soft: []
story_points: 3
submission_type: continue_repo
from_repo: projects/sql/shop-project/part-1
tags:
- sql
- skill/databases
ready: false
title: Shop Database using sql - part 2
---

In the last part of this project you created a Shop Database and performed some SQL queries, now it is time to add more queries.

## Instructions

Create a new branch and ensure your repository maintains the same structure with additional new queries.

### Querying a database

Save all of your instructions in script files.

**NB! Be sure to label your answers by placing the question above the corresponding code. Submitting a wall of code without explanations makes it difficult to review.**

18. Using `DISTINCT`, select all unique cities from the `Customers` table.
19. Using `DISTINCT`, select all unique job titles from the `Employees` table. 
20. Classify `Customers` by `Country` into "Local" or "International".
21. Classify `Orders` into "Completed" or "Pending" based on their status.
22. Select Customer Full Names and Emails with Aliases.
23. Select Products with their names and Price Aliased.
24. With the use of an `INNER JOIN`, create a query that will join `Payments` with `Customers` names using Aliases.
25. With the use of an `INNER JOIN`, create a query that will join `Orders` with `Employees` names using Aliases.

- Ensure the learner has adapted the naming conventions to match those specified in {{< contentlink path="topics/clean-code/sql" >}}