# 🗄️ 11 | SQL Subqueries

**Subquery** হলো একটি SQL query-এর ভিতরে আরেকটি
SQL query ব্যবহার করা।

```text
Main Query
    ↓
  Subquery
    ↓
  Result
```

---

# 🔹 Basic Subquery

যেসব User-এর age-এর চেয়ে বেশি age আছে তাদের খুঁজতে:

```sql
SELECT name, age
FROM users
WHERE age > (
    SELECT AVG(age)
    FROM users
);
```

এখানে:

```sql
SELECT AVG(age)
FROM users
```

হলো **Subquery**।

---

# 🔹 Subquery with `IN`

একটি Table-এর result ব্যবহার করে অন্য Table থেকে
data খোঁজা যায়।

```sql
SELECT name
FROM users
WHERE id IN (
    SELECT user_id
    FROM orders
);
```

এখানে যেসব User-এর Order আছে শুধু তাদের দেখাবে।

```text
orders
  ↓
user_id
  ↓
Subquery
  ↓
users
  ↓
name
```

---

# 🔹 Subquery with `EXISTS`

Related data আছে কিনা check করতে `EXISTS` ব্যবহার করা হয়।

```sql
SELECT name
FROM users
WHERE EXISTS (
    SELECT 1
    FROM orders
    WHERE orders.user_id = users.id
);
```

এখানে যেসব User-এর অন্তত একটি Order আছে
তাদের পাওয়া যাবে।

---

# 🔹 Subquery in `FROM`

Subquery-কে temporary result হিসেবে ব্যবহার করা যায়।

```sql
SELECT *
FROM (
    SELECT name, age
    FROM users
    WHERE age >= 18
) AS adults;
```

এখানে inner query-এর result-কে `adults` নামে
temporary table-এর মতো ব্যবহার করা হয়েছে।

---

# 🔍 Subquery Types

```text
Subquery
   │
   ├── Scalar Subquery
   ├── IN Subquery
   ├── EXISTS Subquery
   └── FROM Subquery
```

### Scalar Subquery

একটি মাত্র value return করে।

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

---

# 🔗 Laravel Connection

Laravel Query Builder-এ Subquery ব্যবহার করা যায়।

```php
$averagePrice = DB::table('products')
    ->selectRaw('AVG(price)');

$products = DB::table('products')
    ->where('price', '>', $averagePrice)
    ->get();
```

`whereIn()` দিয়েও subquery করা যায়:

```php
$userIds = DB::table('orders')
    ->select('user_id');

$users = DB::table('users')
    ->whereIn('id', $userIds)
    ->get();
```

---

# 📝 Practice

### Exercise 01

Average price-এর চেয়ে বেশি price-এর
সব Product খুঁজে বের করো।

### Exercise 02

যেসব User-এর Order আছে তাদের খুঁজে বের করো।

### Exercise 03

`IN` এবং `EXISTS` ব্যবহার করে একই result পাওয়ার
চেষ্টা করো।

---

# 📌 Quick Summary

```text
Subquery
   ↓
Query inside Query
   ↓
Inner Query
   ↓
Result
   ↓
Main Query
```

- `IN` → Multiple values-এর সাথে compare
- `EXISTS` → Related data আছে কিনা check
- `AVG()` → Aggregate result-এর সাথে compare
- `FROM` → Subquery result-কে temporary table হিসেবে ব্যবহার

> 🎯 **Goal:** SQL Subquery বুঝে complex database query
> এবং Laravel Query Builder-এর advanced query বুঝতে পারা।