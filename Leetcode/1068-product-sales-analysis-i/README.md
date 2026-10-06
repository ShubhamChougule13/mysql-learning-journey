# LeetCode 1068 - Product Sales Analysis I

## Problem

Write a solution to report the `product_name`, `year`, and `price` for each `sale_id` in the `Sales` table.

Return the resulting table in any order.

---

# Tables

## 1. Sales

| Column Name | Type | Description |
|---|---|---|
| `sale_id` | int | ID of the sale |
| `product_id` | int | ID of the product |
| `year` | int | Year of the sale |
| `quantity` | int | Quantity sold |
| `price` | int | Price per unit |

The combination of:

```text
(sale_id, year)
