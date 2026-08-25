# 🗄️ 03 | Table Management

SQL-এ existing Table তৈরি, পরিবর্তন, rename এবং delete
করার জন্য বিভিন্ন command ব্যবহার করা হয়।

---

## 🔹 Create Table

নতুন Table তৈরি করতে `CREATE TABLE` ব্যবহার করা হয়।

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE
);
```

---

## 🔹 Show Tables

Database-এর সব Table দেখতে:

```sql
SHOW TABLES;
```

---

## 🔹 Describe Table

Table-এর structure দেখতে:

```sql
DESCRIBE users;
```

অথবা:

```sql
DESC users;
```

---

## 🔹 Add Column

Existing Table-এ নতুন column যোগ করতে:

```sql
ALTER TABLE users
ADD phone VARCHAR(20);
```

---

## 🔹 Modify Column

Existing column-এর data type বা definition পরিবর্তন করতে:

```sql
ALTER TABLE users
MODIFY phone VARCHAR(30);
```

---

## 🔹 Rename Column

Column-এর নাম পরিবর্তন করতে:

```sql
ALTER TABLE users
RENAME COLUMN phone TO mobile;
```

---

## 🔹 Drop Column

একটি column delete করতে:

```sql
ALTER TABLE users
DROP COLUMN mobile;
```

---

## 🔹 Rename Table

Table-এর নাম পরিবর্তন করতে:

```sql
RENAME TABLE users TO customers;
```

---

## 🔹 Drop Table

পুরো Table delete করতে:

```sql
DROP TABLE customers;
```

⚠️ Table এবং এর সব data permanently delete হয়ে যাবে।

---

## 🔗 Laravel Connection

Laravel-এ Table management সাধারণত **Migration** দিয়ে করা হয়।

### Add Column

```php
Schema::table('users', function (Blueprint $table) {
    $table->string('phone');
});
```

Migration run:

```bash
php artisan migrate
```

### Remove Column

```php
Schema::table('users', function (Blueprint $table) {
    $table->dropColumn('phone');
});
```

---

## 📝 Practice

`users` table-এর উপর practice করো:

```text
1. phone column add করো
2. phone → mobile rename করো
3. mobile-এর type change করো
4. mobile column delete করো
5. users → customers rename করো
```

---

## 📌 Quick Summary

```text
CREATE TABLE  → Table তৈরি
SHOW TABLES   → Table দেখা
DESCRIBE      → Structure দেখা
ALTER TABLE   → Table পরিবর্তন
RENAME TABLE  → Table rename
DROP TABLE    → Table delete
```

> 🎯 **Goal:** SQL দিয়ে existing Table manage করতে পারা
> এবং Laravel Migration-এর সাথে এর connection বুঝতে পারা।