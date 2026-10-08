# LeetCode 197 - Rising Temperature

## Problem

Write a solution to find all dates' `id` with higher temperatures compared to their previous dates (yesterday).

Return the result table in any order.

---

# Table

## Weather

| Column Name | Type | Description |
|---|---|---|
| `id` | int | Unique ID of the weather record |
| `recordDate` | date | Date of the weather record |
| `temperature` | int | Temperature on that date |

`id` contains unique values.

There are no different rows with the same `recordDate`.

Each row contains information about the temperature on a certain day.

---

# What Is the Question Actually Asking?

We need to find the `id` of every weather record where:

```text
Today's temperature > Yesterday's temperature
