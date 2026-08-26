# 🗄️ 05 | SQL Constraints

**Constraints** হলো Database-এর Column-এর data-এর উপর
কিছু rules বা restrictions।

এগুলো Database-এর data **valid এবং consistent** রাখতে সাহায্য করে।

---

## 🔹 Common Constraints

```text
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
DEFAULT
CHECK
```

---

## 🔹 PRIMARY KEY

প্রতিটি Row-কে uniquely identify করতে ব্যবহার করা হয়।

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100)
);
```

একই `id` একাধিকবার থাকতে পারবে না।

---

## 🔹 NOT NULL

Column-এ অবশ্যই value থাকতে হবে।

```sql
CREATE TABLE users (
    name VARCHAR(100) NOT NULL
);
```

`name` empty রেখে insert করা যাবে না।

---

## 🔹 UNIQUE

একই value একাধিকবার থাকতে দেয় না।

```sql
CREATE TABLE users (
    email VARCHAR(150) UNIQUE
);
```

একই email দুইজন User ব্যবহার করতে পারবে না।

---

## 🔹 DEFAULT

Value না দিলে default value ব্যবহার করবে।

```sql
CREATE TABLE users (
    status VARCHAR(20) DEFAULT 'active'
);
```

Value না দিলে:

```text
status → active
```

---

## 🔹 CHECK

Data একটি নির্দিষ্ট condition follow করছে কিনা
তা check করে।

```sql
CREATE TABLE users (
    age INT CHECK (age >= 18)
);
```

`18`-এর কম age insert করা যাবে না।

---

## 🔹 FOREIGN KEY

একটি Table-এর Column-কে অন্য Table-এর সাথে
relationship তৈরি করতে ব্যবহার করা হয়।

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

এখানে:

```text
users
  ↓
id

orders
  ↓
user_id
  ↓
FOREIGN KEY
```

---

## 🔗 Laravel Connection

Laravel Migration-এ Constraints সহজেই define করা যায়।

```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->string('status')->default('active');
});
```

Foreign Key:

```php
$table->foreignId('user_id')
      ->constrained('users');
```

---

## 📌 Quick Summary

| Constraint | কাজ |
|---|---|
| `PRIMARY KEY` | Unique row identify |
| `FOREIGN KEY` | Table relationship |
| `NOT NULL` | Value required |
| `UNIQUE` | Duplicate prevent |
| `DEFAULT` | Default value |
| `CHECK` | Condition enforce |

```text
Constraints
     ↓
Data Rules
     ↓
Valid + Consistent Data
```

> 🎯 **Goal:** SQL Constraints বুঝে Laravel Migration-এ
> `unique()`, `default()`, `foreignId()` ইত্যাদি ব্যবহার
> করতে পারা।