# 🗄️ 12 | Views in MySQL

**View** হলো একটি virtual table, যা একটি `SELECT` query-এর
উপর ভিত্তি করে তৈরি করা হয়।

View সাধারণত complex query সহজে reuse করার জন্য ব্যবহার করা হয়।

---

## 🔹 Create View

ধরো `users` table থেকে শুধু active users দেখতে চাই:

```sql
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active';
```

এখন View-টাকে Table-এর মতো query করা যায়:

```sql
SELECT *
FROM active_users;
```

---

## 🔹 View with JOIN

একাধিক Table-এর data combine করেও View তৈরি করা যায়।

```sql
CREATE VIEW user_orders AS
SELECT
    users.id,
    users.name,
    orders.amount
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

তারপর:

```sql
SELECT *
FROM user_orders;
```

Result:

```text
id    name    amount
1     Emon    1000
2     Sakil   2000
```

---

## 🔹 Show Views

Database-এর Views দেখতে:

```sql
SHOW FULL TABLES
WHERE TABLE_TYPE = 'VIEW';
```

---

## 🔹 View Structure

View-এর definition দেখতে:

```sql
SHOW CREATE VIEW active_users;
```

---

## 🔹 Update View

View-এর query পরিবর্তন করতে:

```sql
CREATE OR REPLACE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE status = 'active'
AND id > 10;
```

---

## 🔹 Delete View

View remove করতে:

```sql
DROP VIEW active_users;
```

⚠️ এতে View delete হবে, মূল Table-এর data delete হবে না।

---

## 🔗 Laravel Connection

Laravel Migration-এর মাধ্যমে MySQL View তৈরি করা যায়।

```php
DB::statement("
    CREATE VIEW active_users AS
    SELECT id, name, email
    FROM users
    WHERE status = 'active'
");
```

তারপর View-কে query করা যায়:

```php
$users = DB::table('active_users')->get();
```

---

## 🔍 Table vs View

| Table | View |
|---|---|
| Actual data store করে | Query-এর result দেখায় |
| Physical table | Virtual table |
| Data directly থাকে | Data মূল Table থেকে আসে |
| `CREATE TABLE` | `CREATE VIEW` |

```text
Table
  ↓
Actual Data

View
  ↓
SELECT Query
  ↓
Virtual Table
```

---

## 📝 Practice

### Exercise 01

শুধু active users-এর জন্য একটি View তৈরি করো:

```text
active_users
```

### Exercise 02

`users` এবং `orders` JOIN করে একটি View তৈরি করো:

```text
user_orders
```

### Exercise 03

View-এর:

```text
CREATE
SELECT
UPDATE
DROP
```

সব operation practice করো।

---

## 📌 Quick Summary

```text
CREATE VIEW
     ↓
SELECT Query
     ↓
Virtual Table
     ↓
Reuse Query
```

- `CREATE VIEW` → View তৈরি
- `SELECT` → View থেকে data পাওয়া
- `CREATE OR REPLACE VIEW` → View update
- `DROP VIEW` → View delete
- View delete করলে মূল Table-এর data delete হয় না

> 🎯 **Goal:** MySQL View বুঝে complex query reusable এবং
> সহজে manage করতে পারা।