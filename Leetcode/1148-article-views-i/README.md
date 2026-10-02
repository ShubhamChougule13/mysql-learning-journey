# LeetCode 1148 - Article Views I

## Problem

Find all the authors that viewed at least one of their own articles.

Return the result table sorted by `id` in ascending order.

---

## Table

### Views

| Column Name | Type | Description |
|---|---|---|
| `article_id` | int | ID of the article |
| `author_id` | int | ID of the author who wrote the article |
| `viewer_id` | int | ID of the person who viewed the article |
| `view_date` | date | Date when the article was viewed |

There is no primary key for this table, so duplicate rows may exist.

If `author_id` and `viewer_id` are equal, it means the author viewed their own article.

---

# Understanding the Question

The question asks:

> Find all the authors that viewed at least one of their own articles.

"Own article" means:

```text
author_id = viewer_id
