# LeetCode 1378 - Replace Employee ID With The Unique Identifier

## Problem

Write a solution to show the **unique ID** of each employee.

If an employee does not have a unique ID, replace it with `NULL`.

Return the result table in any order.

---

# Tables

## 1. Employees

| Column Name | Type | Description |
|---|---|---|
| `id` | int | Unique ID of the employee |
| `name` | varchar | Name of the employee |

`id` is the primary key of the `Employees` table.

Each row contains the ID and name of an employee.

---

## 2. EmployeeUNI

| Column Name | Type | Description |
|---|---|---|
| `id` | int | Employee ID |
| `unique_id` | int | Unique identifier of the employee |

The combination of:

```text
(id, unique_id)
