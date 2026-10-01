# LeetCode 595 - Big Countries

## Problem

A country is considered **big** if:

1. It has an area of at least **3,000,000 km²**, OR
2. It has a population of at least **25,000,000**.

Find the **name, population, and area** of all the big countries.

Return the result table in **any order**.

---

## Table

### World

| Column Name | Type | Description |
|---|---|---|
| `name` | varchar | Name of the country |
| `continent` | varchar | Continent to which the country belongs |
| `area` | int | Area of the country in square kilometers |
| `population` | int | Population of the country |
| `gdp` | bigint | GDP value of the country |

`name` is the primary key, so every country name is unique.

---

# Understanding the Question

The question asks us to find **big countries**.

A country is big when **at least one** of the following two conditions is true.

---

## Condition 1 - Area

The country must have an area of **at least 3,000,000 km²**.

The phrase:

> at least 3,000,000

means:

> 3,000,000 or greater.

Therefore:

```sql
area >= 3000000
