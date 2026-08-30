# 🟢 01 | ORM & Eloquent

## 🔹 What is ORM?

ORM-এর full form:

```text
Object Relational Mapping
```

ORM এমন একটি technique যার মাধ্যমে
**Programming Language-এর Object** এবং
**Database-এর Table**-এর মধ্যে connection তৈরি করা হয়।

```text
PHP Object
    ↕
   ORM
    ↕
Database Table
```

---

## 🔹 Without ORM

ধরো MySQL-এ `users` table আছে।

SQL দিয়ে:

```sql
SELECT * FROM users;
```

PHP-তে manually query করতে হয়:

```php
$result = $connection->query(
    "SELECT * FROM users"
);
```

এখানে আমাদের SQL লিখতে হচ্ছে।

---

## 🔹 With ORM

Laravel-এর Eloquent ORM ব্যবহার করলে:

```php
$users = User::all();
```

এখানে:

```text
User
 ↓
Laravel Model

all()
 ↓
Eloquent ORM

MySQL
 ↓
users table
```

Eloquent প্রয়োজনীয় SQL query নিজে তৈরি করে।

Conceptually:

```php
User::all();
```

এর SQL:

```sql
SELECT * FROM users;
```

---

# 🔹 What is Eloquent?

**Eloquent** হলো Laravel-এর built-in ORM।

Eloquent-এর মাধ্যমে Database-এর Table-কে
Laravel Model-এর মাধ্যমে interact করা যায়।

```text
Database Table
      ↕
Eloquent Model
      ↕
PHP Code
```

Example:

```text
users table
     ↕
 User Model
```

---

# 🔹 Model কী?

Laravel-এ Database Table-এর সাথে কাজ করার জন্য
**Model** ব্যবহার করা হয়।

Example:

```php
class User extends Model
{
}
```

এখানে:

```text
User
 ↓
Model
 ↓
users table
```

Laravel convention অনুযায়ী:

```text
User Model
   ↓
users table
```

---

# 🔹 Eloquent Basic Example

```php
use App\Models\User;

$users = User::all();
```

এখানে:

```text
User
 ↓
Model

all()
 ↓
সব users

MySQL
 ↓
users table
```

---

# 🔹 Retrieve One User

```php
$user = User::find(1);
```

Conceptually SQL:

```sql
SELECT *
FROM users
WHERE id = 1
LIMIT 1;
```

---

# 🔹 Create User

```php
$user = User::create([
    'name' => 'Emon',
    'email' => 'emon@example.com',
]);
```

Conceptually SQL:

```sql
INSERT INTO users (name, email)
VALUES ('Emon', 'emon@example.com');
```

---

# 🔹 Update User

```php
$user = User::find(1);

$user->update([
    'name' => 'Mahadi',
]);
```

Conceptually:

```sql
UPDATE users
SET name = 'Mahadi'
WHERE id = 1;
```

---

# 🔹 Delete User

```php
$user = User::find(1);

$user->delete();
```

Conceptually:

```sql
DELETE FROM users
WHERE id = 1;
```

---

# 🔄 SQL vs Eloquent

| SQL | Eloquent |
|---|---|
| `SELECT *` | `Model::all()` |
| `WHERE` | `where()` |
| `INSERT` | `create()` |
| `UPDATE` | `update()` |
| `DELETE` | `delete()` |

Example:

```sql
SELECT *
FROM users
WHERE status = 'active';
```

Eloquent:

```php
User::where('status', 'active')->get();
```

---

# 🧠 Important Concept

Eloquent কোনো আলাদা Database না।

```text
Laravel
   ↓
Eloquent
   ↓
SQL Query
   ↓
MySQL
```

Eloquent মূলত আমাদেরকে
**PHP/Laravel syntax দিয়ে Database-এর সাথে কাজ করার
সহজ interface** দেয়।

---

# 🔗 Laravel Project Flow

একটি real Laravel application-এ সাধারণত:

```text
Request
   ↓
Controller
   ↓
Service
   ↓
Eloquent Model
   ↓
MySQL
   ↓
Result
   ↓
Response
```

---

# 📌 Quick Summary

```text
ORM
 ↓
Object ↔ Database

Eloquent
 ↓
Laravel's ORM

Model
 ↓
Database Table

User Model
 ↓
users Table
```

### Remember

```php
User::all();
```

মানে:

```text
User Model
    ↓
users table
    ↓
Get all records
```

> 🎯 **Goal:** ORM, Eloquent এবং Model-এর relationship
> পরিষ্কারভাবে বুঝতে পারা এবং SQL query-কে Eloquent
> syntax-এর সাথে মিলাতে পারা।