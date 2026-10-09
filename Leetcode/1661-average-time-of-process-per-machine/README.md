# LeetCode 1661 - Average Time of Process per Machine

## Problem

Find the average time each machine takes to complete a process.

The processing time is calculated by subtracting the `start` timestamp from the `end` timestamp.

The average processing time is the total processing time of all processes on a machine divided by the number of processes on that machine.

Round `processing_time` to **3 decimal places**.

Return the result table in any order.

---

## Table Schema

### Activity

| Column | Type | Description |
|---|---|---|
| `machine_id` | int | ID of the machine |
| `process_id` | int | ID of the process |
| `activity_type` | enum | Either `start` or `end` |
| `timestamp` | float | Time of the activity in seconds |

The combination of `machine_id`, `process_id`, and `activity_type` is the primary key.

Every machine-process pair has exactly one `start` record and one `end` record.

---

## Example Input

### Activity

| machine_id | process_id | activity_type | timestamp |
|---:|---:|---|---:|
| 0 | 0 | start | 0.712 |
| 0 | 0 | end | 1.520 |
| 0 | 1 | start | 3.140 |
| 0 | 1 | end | 4.120 |
| 1 | 0 | start | 0.550 |
| 1 | 0 | end | 1.550 |
| 1 | 1 | start | 0.430 |
| 1 | 1 | end | 1.420 |
| 2 | 0 | start | 4.100 |
| 2 | 0 | end | 4.512 |
| 2 | 1 | start | 2.500 |
| 2 | 1 | end | 5.000 |

## Expected Output

| machine_id | processing_time |
|---:|---:|
| 0 | 0.894 |
| 1 | 0.995 |
| 2 | 1.456 |

---

## Understanding the Problem

Each process has two records:

- `start`: when the process begins.
- `end`: when the process finishes.

The processing time is:

`end timestamp - start timestamp`

After calculating each process's duration, we calculate the average duration for each machine.

### Example: Machine 0

Process 0:

`1.520 - 0.712 = 0.808`

Process 1:

`4.120 - 3.140 = 0.980`

Average processing time:

`(0.808 + 0.980) / 2 = 0.894`

Therefore, machine 0 has an average processing time of `0.894`.

---

## Logic

We need to perform five operations:

1. Join the `Activity` table with itself.
2. Match records using `machine_id` and `process_id`.
3. Match the `start` record with the `end` record.
4. Calculate the duration using `end timestamp - start timestamp`.
5. Group by machine, calculate the average, and round it to three decimal places.

### Why Self Join?

The start and end timestamps are stored in separate rows of the same table.

A self join allows us to compare those rows.

We use aliases:

- `a`: start record.
- `b`: end record.

### Why Match Both IDs?

We use:

`a.machine_id = b.machine_id`

to ensure both records belong to the same machine.

We use:

`a.process_id = b.process_id`

to ensure both records belong to the same process.

Without matching the process ID, we could calculate a duration using unrelated processes.

### Why AVG()?

`AVG()` calculates the average of the process durations for each machine.

### Why GROUP BY?

`GROUP BY a.machine_id` ensures the result contains one row per machine.

### Why ROUND(..., 3)?

The question explicitly requires the average to be rounded to three decimal places.

---

## SQL Solution

```sql
SELECT
    a.machine_id,
    ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
FROM Activity a
JOIN Activity b
    ON a.machine_id = b.machine_id
    AND a.process_id = b.process_id
    AND a.activity_type = 'start'
    AND b.activity_type = 'end'
GROUP BY a.machine_id;
```

---

## Step-by-Step Explanation

### Step 1: Join the table with itself

```sql
FROM Activity a
JOIN Activity b
```

We use the same table twice to access the start and end records.

### Step 2: Match the machine and process

```sql
ON a.machine_id = b.machine_id
AND a.process_id = b.process_id
```

This ensures that both records belong to the same process on the same machine.

### Step 3: Identify start and end

```sql
AND a.activity_type = 'start'
AND b.activity_type = 'end'
```

Now `a.timestamp` represents the start time and `b.timestamp` represents the end time.

### Step 4: Calculate processing time

```sql
b.timestamp - a.timestamp
```

Subtract the start timestamp from the end timestamp.

### Step 5: Calculate the average

```sql
AVG(b.timestamp - a.timestamp)
```

Calculate the average duration of the processes on each machine.

### Step 6: Round and name the result

```sql
ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
```

Round the average to three decimal places and name the column `processing_time`.

### Step 7: Group by machine

```sql
GROUP BY a.machine_id
```

Return one average processing time per machine.

---

## Dry Run

| Machine | Process | Start | End | Duration |
|---:|---:|---:|---:|---:|
| 0 | 0 | 0.712 | 1.520 | 0.808 |
| 0 | 1 | 3.140 | 4.120 | 0.980 |
| 1 | 0 | 0.550 | 1.550 | 1.000 |
| 1 | 1 | 0.430 | 1.420 | 0.990 |
| 2 | 0 | 4.100 | 4.512 | 0.412 |
| 2 | 1 | 2.500 | 5.000 | 2.500 |

Average for machine 0:

`(0.808 + 0.980) / 2 = 0.894`

Average for machine 1:

`(1.000 + 0.990) / 2 = 0.995`

Average for machine 2:

`(0.412 + 2.500) / 2 = 1.456`

---

## Common Mistakes

1. **Matching only `machine_id`:** This can pair different processes from the same machine.
2. **Subtracting in the wrong order:** Always calculate `end - start`.
3. **Forgetting `GROUP BY`:** The question requires an average for every machine.
4. **Using `SUM()` instead of `AVG()`:** The question asks for average time, not total time.
5. **Forgetting `ROUND(..., 3)`:** The result must be rounded to three decimal places.
6. **Incorrect activity conditions:** Make sure `a` is `start` and `b` is `end`.

---

## Concepts Learned

- Self Join
- Table aliases
- Joining on multiple columns
- Matching related records
- Conditional row matching
- `AVG()` aggregate function
- `GROUP BY`
- `ROUND()`
- Arithmetic operations in SQL

---

## Problem-Solving Pattern

When a question stores related information in separate rows:

1. Identify how the rows are related.
2. Join the table to itself when appropriate.
3. Match the correct records.
4. Calculate the required value.
5. Group and aggregate if needed.

**Key takeaway:** Use a self join to pair each process's start and end records, then calculate the average processing time for each machine.

---

## LeetCode Details

- **Problem:** 1661 - Average Time of Process per Machine
- **Difficulty:** Medium
- **Language:** MySQL
- **Status:** Accepted
- **Time complexity:** O(n) expected with suitable indexing for the join, subject to the database execution plan.
- **Space complexity:** Depends on the execution plan and intermediate results.

## Final Solution

```sql
SELECT
    a.machine_id,
    ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
FROM Activity a
JOIN Activity b
    ON a.machine_id = b.machine_id
    AND a.process_id = b.process_id
    AND a.activity_type = 'start'
    AND b.activity_type = 'end'
GROUP BY a.machine_id;
```
