# 🗄️ 02 | Data Types in SQL

SQL Data Type নির্ধারণ করে একটি column-এ **কী ধরনের data**
রাখা যাবে।

---

## 🔹 Common SQL Data Types

| Data Type | ব্যবহার | Example |
|---|---|---|
| `INT` | পূর্ণ সংখ্যা | `25` |
| `DECIMAL` | Decimal/টাকার value | `99.99` |
| `VARCHAR` | ছোট/মাঝারি text | `"Emon"` |
| `TEXT` | বড় text | Description |
| `DATE` | Date | `2026-08-25` |
| `DATETIME` | Date + Time | `2026-08-25 15:30:00` |
| `BOOLEAN` | True/False | `1 / 0` |

---

## 🔹 INT

পূর্ণ সংখ্যা রাখার জন্য।

```sql
CREATE TABLE users (
    id INT
);
```

Example:

```text
1
25
100
5000
```

---

## 🔹 VARCHAR

String বা ছোট/মাঝারি text রাখার জন্য।

```sql
CREATE TABLE users (
    name VARCHAR(100),
    email VARCHAR(150)
);
```

Example:

```text
Emon
emon@example.com
```

---

## 🔹 TEXT

বড় text রাখার জন্য।

```sql
CREATE TABLE posts (
    description TEXT
);
```

Example:

```text
This is a long description...
```

---

## 🔹 DECIMAL

Price, salary বা financial value-এর জন্য ব্যবহার করা হয়।

```sql
CREATE TABLE products (
    price DECIMAL(10, 2)
);
```

Example:

```text
999.99
1500.50
```

`DECIMAL(10,2)` মানে মোট 10 digit এবং decimal-এর পরে 2 digit।

---

## 🔹 DATE

শুধু Date রাখার জন্য।

```sql
CREATE TABLE users (
    birth_date DATE
);
```

Example:

```text
2026-08-25
```

---

## 🔹 DATETIME

Date এবং Time দুটোই রাখার জন্য।

```sql
CREATE TABLE appointments (
    appointment_at DATETIME
);
```

Example:

```text
2026-08-25 15:30:00
```

---

## 🔹 BOOLEAN

True/False type data রাখার জন্য।

```sql
CREATE TABLE users (
    is_active BOOLEAN
);
```

MySQL-এ সাধারণত:

```text
1 → TRUE
0 → FALSE
```

---

## 🔗 Laravel Connection

Laravel Migration-এ SQL Data Type-এর জন্য
corresponding methods ব্যবহার করা হয়।

```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->text('bio');
    $table->decimal('salary', 10, 2);
    $table->date('birth_date');
    $table->boolean('is_active');
    $table->dateTime('created_at');
});
```

```text
Laravel Migration
       ↓
Data Type
       ↓
MySQL Column
```

---

## 📝 Practice

একটি `products` table তৈরি করো:

```text
id          → INT
name        → VARCHAR
description → TEXT
price       → DECIMAL
stock       → INT
is_active   → BOOLEAN
created_at  → DATETIME
```

---

## 📌 Quick Summary

```text
INT       → Number
VARCHAR   → String
TEXT      → Large Text
DECIMAL   → Decimal / Money
DATE      → Date
DATETIME  → Date + Time
BOOLEAN   → True / False
```

> 🎯 **Goal:** কোন data-এর জন্য কোন SQL Data Type ব্যবহার
> করতে হবে এবং Laravel Migration-এ তার equivalent কী,
> সেটা বুঝতে পারা।