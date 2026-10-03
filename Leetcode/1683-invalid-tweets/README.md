# LeetCode 1683 - Invalid Tweets

## Problem

Find the IDs of the invalid tweets.

A tweet is considered **invalid** if the number of characters used in its `content` is **strictly greater than 15**.

Return the result table in any order.

---

# Table

### Tweets

| Column Name | Type | Description |
|---|---|---|
| `tweet_id` | int | Unique ID of the tweet |
| `content` | varchar | Content/text of the tweet |

`tweets_id` is the primary key, so every tweet has a unique ID.

---

# Understanding the Question

We need to find tweets whose content contains **more than 15 characters**.

The important part of the question is:

> The tweet is invalid if the number of characters used in the content is **strictly greater than 15**.

Let's break this sentence down.

---

# Condition

We need to calculate the length of the `content`.

In MySQL, we can use:

```sql
LENGTH(content)
