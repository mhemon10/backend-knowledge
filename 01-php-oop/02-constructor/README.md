# 🐘 02 | Constructor & Destructor

PHP OOP-তে **Constructor** এবং **Destructor** Object-এর
lifecycle-এর সাথে কাজ করে।

---

## 🔹 Constructor

Constructor হলো একটি special method, যা Object তৈরি হওয়ার
সময় automatically execute হয়।

PHP-তে Constructor:

```php
__construct()
```

### Example

```php
class User
{
    public string $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$user = new User("Emon");

echo $user->name;
```

### Output

```text
Emon
```

Constructor সাধারণত Object তৈরি হওয়ার সময় initial data
set করার জন্য ব্যবহার করা হয়।

---

## 🔗 Laravel Connection

Laravel-এ Constructor সবচেয়ে বেশি দেখা যায়
**Dependency Injection**-এ।

```php
class UserController extends Controller
{
    public function __construct(
        private UserService $userService
    ) {
    }
}
```

এখানে Laravel `UserService` automatically inject করে।

```text
UserController
      ↓
__construct()
      ↓
UserService
      ↓
Dependency Injection
```

---

## 🔹 Constructor Property Promotion

PHP 8+ এ Constructor আরও short করে লেখা যায়:

```php
class User
{
    public function __construct(
        public string $name,
        public string $email
    ) {
    }
}
```

---

## 🔹 Destructor

Destructor হলো এমন একটি special method, যা Object destroy
হওয়ার সময় execute হয়।

PHP-তে Destructor:

```php
__destruct()
```

### Example

```php
class User
{
    public function __destruct()
    {
        echo "User object destroyed";
    }
}

$user = new User();
```

Destructor সাধারণত **cleanup** কাজের জন্য ব্যবহার করা হয়।

---

## 🔄 Constructor vs Destructor

```text
Object তৈরি
    ↓
__construct()
    ↓
Object ব্যবহার
    ↓
Object destroy
    ↓
__destruct()
```

| Constructor | Destructor |
|---|---|
| `__construct()` | `__destruct()` |
| Object তৈরির সময় চলে | Object destroy হওয়ার সময় চলে |
| Initialization | Cleanup |
| Laravel-এ খুব common | তুলনামূলকভাবে rare |

---

## ⚠️ Common Mistake

❌ ভুল:

```php
public function construct()
{
}
```

✅ সঠিক:

```php
public function __construct()
{
}
```

`__construct()`-এ **দুটি underscore (`__`)** থাকে।

---

## 📝 Practice

### Exercise 01

`User` Class তৈরি করো।

Constructor-এ নাও:

```text
$name
$email
```

তারপর Object তৈরি করে data print করো।

### Exercise 02

`Product` Class তৈরি করো।

Constructor:

```text
$name
$price
$category
```

তারপর Product-এর information print করো।

---

## 📌 Quick Summary

```text
__construct()
    ↓
Object তৈরি হওয়ার সময়
    ↓
Initialize data / Dependency Injection

__destruct()
    ↓
Object destroy হওয়ার সময়
    ↓
Cleanup
```

> 🎯 **Goal:** Constructor ভালোভাবে বুঝে Laravel-এর
> Dependency Injection বুঝতে পারা।