# LeetCode 1581 - Customer Who Visited but Did Not Make Any Transactions

## Problem

Write a solution to find the IDs of the users who visited the mall without making any transactions and the number of times they made these types of visits.

Return the result table in any order.

---

# Tables

## 1. Visits

| Column Name | Type | Description |
|---|---|---|
| `visit_id` | int | Unique ID of the visit |
| `customer_id` | int | ID of the customer |

`visit_id` contains unique values.

Each row represents a customer visiting the mall.

---

## 2. Transactions

| Column Name | Type | Description |
|---|---|---|
| `transaction_id` | int | Unique ID of the transaction |
| `visit_id` | int | ID of the visit during which the transaction happened |
| `amount` | int | Transaction amount |

`transaction_id` contains unique values.

Each row represents a transaction made during a particular visit.

---

# What Is the Question Actually Asking?

We need to find customers who:

1. Visited the mall.
2. Did **not** make any transaction during that visit.
3. Count how many such visits each customer made.

The output must contain:

```text
customer_id
count_no_trans
