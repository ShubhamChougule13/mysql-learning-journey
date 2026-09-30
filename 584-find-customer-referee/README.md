# LeetCode 584 - Find Customer Referee

## Problem

Find the names of customers who are either:

1. Referred by a customer whose ID is not 2.
2. Not referred by any customer.

## Table

### Customer

| Column | Description |
|---|---|
| id | Unique ID of the customer |
| name | Name of the customer |
| referee_id | ID of the customer who referred them |

## Logic

There are two conditions.

### Condition 1

The customer was referred by someone whose ID is not 2:

```sql
referee_id != 2
