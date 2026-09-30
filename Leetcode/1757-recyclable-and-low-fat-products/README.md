# LeetCode 1757 - Recyclable and Low Fat Products

## Problem

Find the IDs of products that are both low fat and recyclable.

## Table

### Products

| Column | Description |
|---|---|
| product_id | Unique ID of the product |
| low_fats | Y = low fat, N = not low fat |
| recyclable | Y = recyclable, N = not recyclable |

## Logic

The question asks for products that satisfy **both** conditions:

1. `low_fats = 'Y'`
2. `recyclable = 'Y'`

Because both conditions must be true, we use `AND`.

## SQL Solution

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
AND recyclable = 'Y';
