# 🗄️ 06 | MySQL Functions

**MySQL Function** হলো এমন একটি built-in বা custom function,
যা data-এর উপর নির্দিষ্ট কাজ করে এবং একটি result return করে।

---

## 🔹 String Functions

### `CONCAT()`

একাধিক string একসাথে করতে ব্যবহার করা হয়।

```sql
SELECT CONCAT('Mahadi', ' ', 'Emon') AS full_name;
```

### Output

```text
Mahadi Emon
```

---

### `UPPER()`

Text uppercase করতে:

```sql
SELECT UPPER('emon') AS name;
```

### Output

```text
EMON
```

---

### `LOWER()`

Text lowercase করতে:

```sql
SELECT LOWER('EMON') AS name;
```

### Output

```text
emon
```

---

## 🔹 Numeric Functions

### `ROUND()`

Decimal number round করতে:

```sql
SELECT ROUND(99.567, 2);
```

### Output

```text
99.57
```

---

### `ABS()`

Negative number-এর positive value পেতে:

```sql
SELECT ABS(-100);
```

### Output

```text
100
```

---

## 🔹 Date Functions

### `CURDATE()`

বর্তমান Date পেতে:

```sql
SELECT CURDATE();
```

### `NOW()`

বর্তমান Date এবং Time পেতে:

```sql
SELECT NOW();
```

---

## 🔹 Aggregate Functions

একাধিক Row-এর data থেকে calculation করতে ব্যবহার করা হয়।

### `COUNT()`

```sql
SELECT COUNT(*) AS total_users
FROM users;
```

---

### `SUM()`

```sql
SELECT SUM(price) AS total_price
FROM products;
```

---

### `AVG()`

```sql
SELECT AVG(price) AS average_price
FROM products;
```

---

### `MAX()` / `MIN()`

```sql
SELECT MAX(price) AS highest_price
FROM products;

SELECT MIN(price) AS lowest_price
FROM products;
```

---

## 🔗 Laravel Connection

Laravel Query Builder / Eloquent-এর মাধ্যমে
MySQL functions ব্যবহার করা যায়।

```php
$users = User::selectRaw(
    'COUNT(*) as total_users'
)->first();
```

এখানে Laravel-এর মাধ্যমে MySQL-এর:

```sql
COUNT(*)
```

function ব্যবহার করা হয়েছে।

---

## 📌 Quick Summary

| Function | কাজ |
|---|---|
| `CONCAT()` | String combine |
| `UPPER()` | Uppercase |
| `LOWER()` | Lowercase |
| `ROUND()` | Number round |
| `ABS()` | Absolute value |
| `CURDATE()` | Current date |
| `NOW()` | Current date & time |
| `COUNT()` | Count rows |
| `SUM()` | Total |
| `AVG()` | Average |
| `MAX()` | Maximum |
| `MIN()` | Minimum |

> 🎯 **Goal:** Common MySQL Functions বুঝে data query-এর
> মধ্যে calculation এবং transformation করতে পারা।