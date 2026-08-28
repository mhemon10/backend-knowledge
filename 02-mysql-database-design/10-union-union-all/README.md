# 🗄️ 10 | UNION & UNION ALL

`UNION` এবং `UNION ALL` ব্যবহার করে একাধিক `SELECT`
query-এর result একসাথে combine করা যায়।

---

# 🔹 UNION

`UNION` multiple query-এর result combine করে এবং
**duplicate rows remove করে**।

```sql
SELECT name FROM customers
UNION
SELECT name FROM suppliers;
```

### Result

```text
name
---------
Emon
Sakil
Rahim
```

একই name একাধিক query-তে থাকলে একবারই দেখাবে।

---

# 🔹 UNION ALL

`UNION ALL` multiple query-এর result combine করে কিন্তু
**duplicate rows remove করে না**।

```sql
SELECT name FROM customers
UNION ALL
SELECT name FROM suppliers;
```

### Result

```text
name
---------
Emon
Sakil
Emon
Rahim
```

এখানে `Emon` দুইবার আছে, কারণ duplicate রাখা হয়েছে।

---

# 🔍 UNION vs UNION ALL

| UNION | UNION ALL |
|---|---|
| Duplicate remove করে | Duplicate রাখে |
| তুলনামূলকভাবে slower | তুলনামূলকভাবে faster |
| Unique result দরকার হলে | সব result দরকার হলে |

```text
UNION
  ↓
Combine
  ↓
Remove Duplicates

UNION ALL
  ↓
Combine
  ↓
Keep Duplicates
```

---

# 🔹 Important Rule

`UNION` ব্যবহার করা SELECT query-গুলোর:

- Column সংখ্যা একই হতে হবে
- Corresponding column-এর data type compatible হতে হবে

Example:

```sql
SELECT name, email FROM users
UNION
SELECT name, email FROM customers;
```

দুই query-তেই **2টি column** আছে।

---

# 🔗 Laravel Connection

Laravel Query Builder-এ `union()` ব্যবহার করা যায়।

```php
$users = DB::table('users')
    ->select('name');

$customers = DB::table('customers')
    ->select('name');

$result = $users->union($customers)->get();
```

`UNION ALL` প্রয়োজন হলে:

```php
$result = $users
    ->unionAll($customers)
    ->get();
```

---

# 📝 Practice

### Exercise 01

`customers` এবং `suppliers` Table থেকে `name` নিয়ে:

```text
UNION
UNION ALL
```

দুটো practice করো।

### Exercise 02

দুইটি Table থেকে `name` এবং `email` combine করো।

তারপর দেখো duplicate data-এর ক্ষেত্রে
`UNION` এবং `UNION ALL` কীভাবে আলাদা result দেয়।

---

# 📌 Quick Summary

```text
UNION
  → Combine + Remove Duplicates

UNION ALL
  → Combine + Keep Duplicates
```

> 🎯 **Goal:** `UNION` এবং `UNION ALL`-এর পার্থক্য বুঝে
> multiple SELECT result efficiently combine করতে পারা।