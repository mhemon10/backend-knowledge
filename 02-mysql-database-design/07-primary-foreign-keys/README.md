# 🗄️ 08 | Primary Key, Auto Increment & Foreign Key

Database-এর Row uniquely identify এবং Table-এর মধ্যে
relationship তৈরি করার জন্য **Primary Key** এবং
**Foreign Key** ব্যবহার করা হয়।

---

# 🔹 Primary Key

**Primary Key** প্রতিটি Row-কে uniquely identify করে।

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

একই `id` দুইটি Row-তে থাকতে পারবে না।

```text
id
1  → Emon
2  → Sakil
3  → Rahim
```

---

# 🔹 Auto Increment

নতুন Row insert হলে `id` automatically বাড়ানোর জন্য
`AUTO_INCREMENT` ব্যবহার করা হয়।

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100)
);
```

Insert:

```sql
INSERT INTO users (name)
VALUES ('Emon');

INSERT INTO users (name)
VALUES ('Sakil');
```

Result:

```text
id    name
1     Emon
2     Sakil
```

---

# 🔹 Foreign Key

**Foreign Key** একটি Table-এর Column-কে অন্য Table-এর
Primary Key-এর সাথে connect করে।

Example:

```text
users
---------
id
name

orders
---------
id
user_id
```

এখানে `orders.user_id` → `users.id`-কে reference করবে।

---

## 🔹 Foreign Key Example

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100)
);
```

তারপর:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,

    FOREIGN KEY (user_id)
    REFERENCES users(id)
);
```

Relationship:

```text
users
  │
  │ id
  ↓
orders
  │
  │ user_id
  └──────────→ users.id
```

---

# 🔹 Insert Related Data

প্রথমে User:

```sql
INSERT INTO users (name)
VALUES ('Emon');
```

তারপর সেই User-এর Order:

```sql
INSERT INTO orders (user_id)
VALUES (1);
```

এখানে:

```text
users.id = 1
       ↓
orders.user_id = 1
```

---

## 🔗 Laravel Connection

Laravel Migration-এ:

```php
Schema::create('users', function (Blueprint $table) {
    $table->id();
    $table->string('name');
});
```

Foreign Key:

```php
Schema::create('orders', function (Blueprint $table) {
    $table->id();

    $table->foreignId('user_id')
          ->constrained('users');
});
```

Laravel-এর:

```php
$table->id();
```

সাধারণত Primary Key + Auto Increment ID তৈরি করে।

---

# 📌 Quick Summary

| Concept | কাজ |
|---|---|
| `PRIMARY KEY` | Row uniquely identify |
| `AUTO_INCREMENT` | ID automatically increase |
| `FOREIGN KEY` | Table relationship তৈরি |
| `REFERENCES` | অন্য Table-এর Key reference |

```text
Primary Key
     ↓
Unique Identity

Auto Increment
     ↓
Automatic ID

Foreign Key
     ↓
Table Relationship
```

> 🎯 **Goal:** Primary Key, Auto Increment এবং Foreign Key
> বুঝে Laravel Migration-এ Table relationship তৈরি করতে পারা।