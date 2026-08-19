# 🐘 03 | Inheritance

**Inheritance** হলো এমন একটি OOP feature যার মাধ্যমে একটি
Class অন্য একটি Class-এর properties এবং methods ব্যবহার করতে পারে।

PHP-তে Inheritance-এর জন্য `extends` keyword ব্যবহার করা হয়।

---

## 🔹 Basic Example

```php
class User
{
    public function login(): string
    {
        return "User logged in";
    }
}

class Admin extends User
{
    public function accessDashboard(): string
    {
        return "Dashboard accessed";
    }
}

$admin = new Admin();

echo $admin->login();
echo "\n";
echo $admin->accessDashboard();
```

### Output

```text
User logged in
Dashboard accessed
```

এখানে:

```text
User
  ↓
Parent Class

Admin
  ↓
Child Class
```

`Admin` class, `User` class-এর `login()` method ব্যবহার করতে
পারছে।

---

## 🔹 `extends`

Inheritance তৈরি করতে `extends` ব্যবহার করা হয়।

```php
class Admin extends User
{
}
```

এখানে:

- `User` → Parent Class
- `Admin` → Child Class

---

## 🔗 Laravel Connection

Laravel-এ Inheritance অনেক জায়গায় ব্যবহার হয়।

### Model

```php
class User extends Model
{
}
```

এখানে:

```text
User
 ↓
extends
 ↓
Model
```

### Controller

```php
class UserController extends Controller
{
}
```

এখানেও `UserController` parent `Controller` class-এর
functionality ব্যবহার করছে।

---

## 🔹 Method Override

Child Class চাইলে Parent Class-এর method নিজের মতো
করে define করতে পারে।

```php
class User
{
    public function role(): string
    {
        return "User";
    }
}

class Admin extends User
{
    public function role(): string
    {
        return "Admin";
    }
}

$admin = new Admin();

echo $admin->role();
```

### Output

```text
Admin
```

এটাকে **Method Overriding** বলা হয়।

---

## 🔹 `parent::`

Child Class থেকে Parent Class-এর method call করতে
`parent::` ব্যবহার করা যায়।

```php
class User
{
    public function login(): string
    {
        return "User login";
    }
}

class Admin extends User
{
    public function login(): string
    {
        return parent::login() . " + Admin access";
    }
}

$admin = new Admin();

echo $admin->login();
```

### Output

```text
User login + Admin access
```

---

## ⚠️ Common Mistake

❌ ভুল:

```php
class Admin -> User
{
}
```

✅ সঠিক:

```php
class Admin extends User
{
}
```

---

## 📝 Practice

### Exercise 01

`Animal` নামে একটি Parent Class তৈরি করো।

Method:

```text
eat()
```

তারপর `Dog` Class তৈরি করে `Animal` থেকে inherit করো।

---

### Exercise 02

`User` থেকে:

```text
Admin
Manager
Customer
```

তিনটি Child Class তৈরি করো।

প্রতিটি Class-এ নিজের একটি আলাদা method যোগ করো।

---

## 📌 Quick Summary

```text
Inheritance
     ↓
Parent Class
     ↓
extends
     ↓
Child Class
```

- `extends` → Inheritance তৈরি করে
- Parent Class → Base Class
- Child Class → Parent-এর functionality ব্যবহার করতে পারে
- Method Override → Child নিজের implementation দিতে পারে
- `parent::` → Parent-এর method access করতে পারে

> 🎯 **Goal:** PHP Inheritance বুঝে Laravel-এর
> `User extends Model` এবং `Controller extends Controller`
> ধরনের structure বুঝতে পারা।