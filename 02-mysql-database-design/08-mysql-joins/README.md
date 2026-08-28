# 🗄️ 09 | MySQL Joins

**JOIN** ব্যবহার করে একাধিক Table-এর related data
একসাথে পাওয়া যায়।

ধরো:

```text
users
---------
id
name

orders
---------
id
user_id
amount
```

`orders.user_id` → `users.id`

---

# 🔹 INNER JOIN

দুই Table-এ matching data থাকলেই result দেখায়।

```sql
SELECT users.name, orders.amount
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```

### Result

```text
name    amount
Emon    1000
Sakil   2000
```

```text
users ───── INNER JOIN ───── orders
         matching rows
```

---

# 🔹 LEFT JOIN

Left Table-এর **সব data** দেখায়।

Matching data না থাকলে right Table-এর value `NULL` হবে।

```sql
SELECT users.name, orders.amount
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id;
```

```text
users
  ↓
সব User দেখাবে
  ↓
Order থাকলে → amount
Order না থাকলে → NULL
```

---

# 🔹 RIGHT JOIN

Right Table-এর **সব data** দেখায়।

```sql
SELECT users.name, orders.amount
FROM users
RIGHT JOIN orders
    ON users.id = orders.user_id;
```

---

# 🔹 Multiple Tables JOIN

একাধিক Table একসাথে JOIN করা যায়।

```sql
SELECT
    users.name,
    orders.amount,
    products.name AS product
FROM users
INNER JOIN orders
    ON users.id = orders.user_id
INNER JOIN products
    ON orders.product_id = products.id;
```

---

# 🔍 JOIN Comparison

| JOIN | কী দেখায় |
|---|---|
| `INNER JOIN` | শুধু matching data |
| `LEFT JOIN` | Left-এর সব + matching Right |
| `RIGHT JOIN` | Right-এর সব + matching Left |

```text
INNER JOIN
    ↓
Only Matching

LEFT JOIN
    ↓
All Left + Matching Right

RIGHT JOIN
    ↓
All Right + Matching Left
```

---

# 🔗 Laravel Connection

Laravel Eloquent Relationship:

```php
$user->orders;
```

Query Builder:

```php
$users = DB::table('users')
    ->join('orders', 'users.id', '=', 'orders.user_id')
    ->select('users.name', 'orders.amount')
    ->get();
```

এখানে Laravel-এর:

```php
->join()
```

MySQL-এর `JOIN` ব্যবহার করে।

---

# 📝 Practice

`users` এবং `orders` Table ব্যবহার করে:

1. `INNER JOIN` দিয়ে User + Order দেখাও
2. `LEFT JOIN` দিয়ে সব User দেখাও
3. যেসব User-এর কোনো Order নেই তাদের খুঁজে বের করো
4. User অনুযায়ী Order amount দেখাও

---

# 📌 Quick Summary

```text
JOIN
  ↓
Multiple Tables
  ↓
Related Data
  ↓
Single Result
```

> 🎯 **Goal:** MySQL JOIN বুঝে Laravel Query Builder এবং
> Eloquent Relationship-এর database queries বুঝতে পারা।