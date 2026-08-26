# 🗄️ 04 | CRUD

**CRUD** হলো Database-এর basic 4টি operation:

```text
C → Create
R → Read
U → Update
D → Delete
```

---

## 🔹 Create

নতুন data insert করতে `INSERT` ব্যবহার করা হয়।

```sql
INSERT INTO users (name, email)
VALUES ('Emon', 'emon@example.com');
```

---

## 🔹 Read

Database থেকে data দেখতে `SELECT` ব্যবহার করা হয়।

```sql
SELECT * FROM users;
```

নির্দিষ্ট column:

```sql
SELECT name, email
FROM users;
```

---

## 🔹 Update

Existing data পরিবর্তন করতে `UPDATE` ব্যবহার করা হয়।

```sql
UPDATE users
SET name = 'Mahadi'
WHERE id = 1;
```

⚠️ `WHERE` ছাড়া `UPDATE` করলে সব row update হয়ে যেতে পারে।

---

## 🔹 Delete

Data delete করতে `DELETE` ব্যবহার করা হয়।

```sql
DELETE FROM users
WHERE id = 1;
```

⚠️ `WHERE` ছাড়া `DELETE` করলে সব data delete হয়ে যেতে পারে।

---

## 🔄 CRUD Flow

```text
Create
  ↓
INSERT
  ↓
Read
  ↓
SELECT
  ↓
Update
  ↓
UPDATE
  ↓
Delete
  ↓
DELETE
```

---

## 🔗 Laravel Connection

Laravel Eloquent-এ CRUD আরও সহজভাবে করা যায়।

### Create

```php
User::create([
    'name' => 'Emon',
    'email' => 'emon@example.com',
]);
```

### Read

```php
$users = User::all();
```

### Update

```php
$user = User::find(1);

$user->update([
    'name' => 'Mahadi',
]);
```

### Delete

```php
$user = User::find(1);

$user->delete();
```

---

## 📌 SQL → Laravel

| SQL | Laravel Eloquent |
|---|---|
| `INSERT` | `create()` |
| `SELECT` | `all()`, `find()` |
| `UPDATE` | `update()` |
| `DELETE` | `delete()` |

---

## 📝 Practice

`users` table-এর উপর:

1. একটি User create করো
2. সব User read করো
3. একজন User update করো
4. একজন User delete করো

তারপর একই CRUD operation Laravel Eloquent দিয়ে
practice করো।

---

> 🎯 **Goal:** SQL-এর CRUD এবং Laravel Eloquent-এর
> CRUD operation-এর connection পরিষ্কারভাবে বুঝতে পারা।