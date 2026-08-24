# 🐘 05 | Abstract Class

**Abstract Class** হলো এমন একটি Class যেটা সরাসরি Object
তৈরি করার জন্য ব্যবহার করা যায় না।

এটি সাধারণত অন্য Class-এর জন্য **base/blueprint** হিসেবে
ব্যবহার করা হয়।

PHP-তে `abstract` keyword ব্যবহার করা হয়।

---

## 🔹 Basic Example

```php
abstract class User
{
    abstract public function getRole(): string;

    public function login(): string
    {
        return "User logged in";
    }
}

class Admin extends User
{
    public function getRole(): string
    {
        return "Admin";
    }
}

$admin = new Admin();

echo $admin->login();
echo "\n";
echo $admin->getRole();
```

### Output

```text
User logged in
Admin
```

---

## ❌ Abstract Class-এর Object তৈরি করা যায় না

```php
abstract class User
{
}

$user = new User();
```

এটা কাজ করবে না।

```text
Abstract Class
      ↓
Cannot create Object
      ↓
Child Class
      ↓
Object তৈরি করা যায়
```

---

## 🔹 Abstract Method

Abstract Class-এর ভিতরে Abstract Method থাকতে পারে।

```php
abstract class Payment
{
    abstract public function pay(float $amount): string;
}
```

Child Class-কে এই method অবশ্যই implement করতে হবে।

```php
class StripePayment extends Payment
{
    public function pay(float $amount): string
    {
        return "Paid $amount using Stripe";
    }
}
```

---

## 🔗 Laravel Connection

Laravel-এ Abstract Class বিভিন্ন জায়গায়
**base functionality** তৈরি করতে ব্যবহার করা যায়।

Example:

```php
abstract class BaseService
{
    public function response(array $data)
    {
        return $data;
    }
}
```

তারপর:

```php
class UserService extends BaseService
{
}
```

এখানে:

```text
BaseService
     ↓
abstract class
     ↓
UserService
     ↓
extends
```

---

## 🔍 Abstract Class vs Normal Class

| Abstract Class | Normal Class |
|---|---|
| Direct Object তৈরি করা যায় না | Object তৈরি করা যায় |
| `abstract` keyword | সাধারণ `class` |
| Base/Blueprint হিসেবে ব্যবহৃত | Directly ব্যবহার করা যায় |
| Abstract Method থাকতে পারে | Abstract Method থাকতে পারে না |

---

## 📝 Practice

### Exercise 01

একটি abstract `Animal` Class তৈরি করো।

Method:

```php
abstract public function sound(): string;
```

তারপর:

```text
Dog
Cat
```

দুটি Class তৈরি করে `sound()` implement করো।

---

### Exercise 02

একটি abstract `Payment` Class তৈরি করো।

তারপর:

```text
StripePayment
SSLCommerzPayment
```

দুটি Child Class তৈরি করো।

---

## 📌 Quick Summary

```text
Abstract Class
      ↓
Base / Blueprint
      ↓
Cannot create Object
      ↓
Child Class
      ↓
Implement Abstract Methods
```

- `abstract` keyword ব্যবহার করা হয়
- Abstract Class থেকে সরাসরি Object তৈরি করা যায় না
- Abstract Method-এর body থাকে না
- Child Class-কে Abstract Method implement করতে হয়
- Common/base functionality রাখার জন্য ব্যবহার করা হয়

> 🎯 **Goal:** Abstract Class বুঝে Laravel-এর service architecture
> এবং interface/abstraction-based design বুঝতে পারা।