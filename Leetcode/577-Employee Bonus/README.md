# LeetCode 577 - Employee Bonus

## Problem

Report the name and bonus amount of each employee who satisfies either condition:

1. The employee has a bonus less than `1000`.
2. The employee did not receive any bonus.

Return the result table in any order.

---

## Table Schema

### Employee

| Column | Type | Description |
|---|---|---|
| `empId` | int | Unique employee ID |
| `name` | varchar | Employee name |
| `supervisor` | int | Employee's supervisor ID |
| `salary` | int | Employee's salary |

### Bonus

| Column | Type | Description |
|---|---|---|
| `empId` | int | Employee ID |
| `bonus` | int | Employee's bonus amount |

The `empId` column in `Bonus` references the `Employee` table.

---

## Example Input

### Employee

| empId | name | supervisor | salary |
|---:|---|---:|---:|
| 3 | Brad | NULL | 4000 |
| 1 | John | 3 | 1000 |
| 2 | Dan | 3 | 2000 |
| 4 | Thomas | 3 | 4000 |

### Bonus

| empId | bonus |
|---:|---:|
| 2 | 500 |
| 4 | 2000 |

## Expected Output

| name | bonus |
|---|---:|
| Brad | NULL |
| John | NULL |
| Dan | 500 |

Thomas is excluded because his bonus is `2000`, which is not less than `1000`.

---

## Understanding the Problem

We need the employee's name and bonus amount.

The information is stored in two different tables:

- `Employee` contains employee names.
- `Bonus` contains bonus amounts.

We connect these tables using `empId`.

We must include employees who have no matching bonus record. Their bonus should appear as `NULL`.

---

## Logic

### Step 1: Join the tables

We use `LEFT JOIN` because all employees must be retained, even when they have no bonus record.

```sql
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
```

### Step 2: Find bonuses below 1000

```sql
b.bonus < 1000
```

This condition includes employees such as Dan, whose bonus is `500`.

### Step 3: Include employees without bonuses

```sql
b.bonus IS NULL
```

When an employee has no matching row in `Bonus`, the joined bonus value is `NULL`.

### Step 4: Combine both conditions

The question says employees must satisfy either condition, so we use `OR`.

```sql
WHERE b.bonus < 1000
   OR b.bonus IS NULL
```

---

## SQL Solution

```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```

---

## Step-by-Step Explanation

### SELECT

```sql
SELECT e.name, b.bonus
```

Return the employee's name and bonus amount.

### FROM

```sql
FROM Employee e
```

Start with the employee records.

### LEFT JOIN

```sql
LEFT JOIN Bonus b
    ON e.empId = b.empId
```

Match employees to their bonuses using the employee ID. Employees without a matching bonus are retained.

### WHERE

```sql
WHERE b.bonus < 1000
   OR b.bonus IS NULL
```

Keep employees whose bonus is below `1000` or whose bonus is missing.

---

## Dry Run

| Employee | Bonus | Bonus below 1000? | Bonus is NULL? | Included? |
|---|---:|---|---|---|
| Brad | NULL | No | Yes | Yes |
| John | NULL | No | Yes | Yes |
| Dan | 500 | Yes | No | Yes |
| Thomas | 2000 | No | No | No |

The final output contains Brad, John, and Dan.

---

## Why LEFT JOIN Instead of INNER JOIN?

`INNER JOIN` returns only employees with matching bonus records.

It would exclude Brad and John, even though the question requires them.

`LEFT JOIN` retains all employees and fills unmatched bonus columns with `NULL`.

---

## Common Mistakes

1. **Using `INNER JOIN`:** Employees without bonuses would disappear.
2. **Using `AND` instead of `OR`:** The two required conditions are alternatives.
3. **Using `= NULL`:** Use `IS NULL` to check for missing values.
4. **Forgetting the join condition:** Match the tables using `empId`.
5. **Using the wrong comparison:** The question says less than `1000`, not less than or equal to `1000`.

---

## Regular Solution

```sql
SELECT Employee.name, Bonus.bonus
FROM Employee
LEFT JOIN Bonus
    ON Employee.empId = Bonus.empId
WHERE Bonus.bonus < 1000
   OR Bonus.bonus IS NULL;
```

## Recommended Solution

```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```

Both solutions produce the same result. Short aliases make the query easier to read and write.

---

## Concepts Learned

- `LEFT JOIN`
- Table aliases
- Joining tables using a common key
- `WHERE`
- `OR`
- `IS NULL`
- Handling missing related records

---

## Problem-Solving Pattern

When a question asks for records from one table, including those without a match in another table:

1. Identify the two tables.
2. Identify the common key.
3. Use `LEFT JOIN` if unmatched records must remain.
4. Apply the required conditions using `WHERE`.
5. Use `OR` when either condition is sufficient.

**Key takeaway:** Use `LEFT JOIN` to retain employees without bonuses, then filter using `bonus < 1000 OR bonus IS NULL`.

---

## LeetCode Details

- **Problem:** 577 - Employee Bonus
- **Difficulty:** Easy
- **Language:** MySQL
- **Status:** Accepted
- **Time complexity:** Depends on the execution plan and available indexes.
- **Space complexity:** Depends on the join execution plan.

---

## Final Solution

```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus < 1000
   OR b.bonus IS NULL;
```
