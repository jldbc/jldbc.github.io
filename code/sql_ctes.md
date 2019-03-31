---
layout: archive
title: "Simplify your SQL Queries with Common Table Expressions (CTEs)"
permalink: /code/sql-cte-common-table-expressions
author_profile: true
redirect_from:
  - /sql-cte-common-table-expressions
---

{% include base_path %}

Writing SQL in a professional setting is never as simple as the tutorials make it out to be. You'll reference several tables, each of which may require custom business logic in order to make them usable. To keep your code readable to yourself and others, consider using **Common Table Expressions**, or CTEs, to avoid packing too much logic into subqueries.

A CTE is a query whose result set you can reference in a later section of your query. It's sort of like a view that's local to the query that it lives in. Instead of writing a large subquery and having your logic nested within an outer query, you can write the subquery as a common table expression that a further section of your query can reference. The result is that the overall query is more modular and significantly easier to edit and understand. 

The syntax of a CTE is simple:

> **`WITH my_cte_name AS (SELECT * FROM EXAMPLE)`**

After you write this CTE, you can reference its result set further down in the query by selecting from result set `my_cte_name` as if it were a table in the database. Here's a more concrete example showing how a complex query can be easier to read, write, and maintain using CTEs.

# Example with Real Data

Here I'll use the [Stack Overflow dataset](https://bigquery.cloud.google.com/dataset/bigquery-public-data:stackoverflow) from Google's public BigQuery data. My goal is to find Stack Overflow users who are experienced in machine learning in Python, which I'll define as the subset of users who have received upvotes on answers they've submitted to questions tagged with both `python` and `machine-learning`. I'll want to know how many of these comments they've submitted as a proxy for how skilled or involved in the ML community they are, and I'll also want to know some general info about who they are (name, location, etc.).

There are three tables needed to answer this. `stackoverflow_posts` contains every post, its unique id, and tags identifying the subject matter. `comments` has each comment id, the commenter's user id, the number of upvotes it received, and the id of the Stack Overflow question it belogs to. Last, `users` has user metadata saying who the user is. 

# Solving This with CTEs

This question can be broken into three questions, which will help to organize it into common table expressions. 

1: which posts are asking questions about machine learning in Python?

2: which comments belong to these ML posts, and which of these comments received at least one upvote?

3: who are the users who submitted upvoted comments to these machine learning posts, and how many of these successful comments have they submitted?

I'll answer the first question with a CTE. The results from the first CTE will then allow me to answer the second question by querying the `comments` table in a second CTE. Finally, I can inner join the second CTE onto the `users` table to answer my initial question of which users are most successful in answering Stack Overflow questions about Machine Learning in Python.

```sql
#StandardSQL
-- find posts about machine learning in python
WITH python_ml_posts AS (
  SELECT
    id
  FROM
    `bigquery-public-data.stackoverflow.stackoverflow_posts`
  WHERE
    tags LIKE '%machine-learning%'
  AND
    tags LIKE '%python%'
),

-- find comments on these ML posts with >0 upvotes and the commenter's user id
ml_post_comments AS (
  SELECT
    user_id,
    count(*) AS comment_count
  FROM
    `bigquery-public-data.stackoverflow.comments` comments
  INNER JOIN
    python_ml_posts
  ON
    python_ml_posts.id = comments.post_id
  WHERE
    score > 0
  GROUP BY
    user_id
)

-- connect users with their machine-learning-comment-count
SELECT
  users.display_name, 
  users.location,
  users.reputation,
  ml_post_comments.comment_count
FROM
  `bigquery-public-data.stackoverflow.users` users
INNER JOIN
  ml_post_comments
ON
  ml_post_comments.user_id = users.id
ORDER BY
  comment_count desc
```

**Row**|**display\_name**|**location**|**reputation**|**comment\_count**| 
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
1|Fred Foo| |281432|30| 
2|Andreas Mueller|New York, United States|14857|21| 
3|lejlot|London, United Kingdom|47420|20| 
4|EdChum|Berkshire, United Kingdom|178578|17| 
5|ogrisel|Paris, France|29009|13| 

This is a fairly complicated question, but as you can see from the above query, it's easy to read and write when you tackle it with CTEs. The alternative would be to query the users table, then join on the comments table with a subquery for finding each user's comments, which in turn would need a **second** subquery for finding which of these comments were related to machine learning in Python. Gross! Don't do that. Use common table expressions instead. Your future self and whoever you share a code base with will thank you.

