# 🐘 04 | Access Modifier

**Access Modifier** দিয়ে Class-এর Property এবং Method
কোথা থেকে access করা যাবে তা control করা হয়।

PHP-তে প্রধান ৩টি Access Modifier:

```text
public
private
protected
```

---

## 🔹 Public

`public` হলে Property বা Method যেকোনো জায়গা থেকে access করা যায়।

```php
class User
{
    public string $name;

    public function login(): string
    {
        return "User logged in";
    }
}

$user = new User();

$user->name = "Emon";

echo $user->name;
echo $user->login();
```

### Output

```text
Emon
User logged in
```

---

## 🔹 Private

`private` হলে শুধু **নিজের Class-এর ভিতর** থেকে access করা যায়।

```php
class User
{
    private string $password = "123456";

    public function getPassword(): string
    {
        return $this->password;
    }
}

$user = new User();

echo $user->getPassword();
```

### Output

```text
123456
```

❌ বাইরে থেকে সরাসরি access করা যাবে না:

```php
echo $user->password;
```

---

## 🔹 Protected

`protected` হলে:

- নিজের Class থেকে access করা যায়
- Child Class থেকেও access করা যায়
- বাইরে থেকে সরাসরি access করা যায় না

```php
class User
{
    protected string $role = "user";
}

class Admin extends User
{
    public function getRole(): string
    {
        return $this->role;
    }
}

$admin = new Admin();

echo $admin->getRole();
```

### Output

```text
user
```

---

## 🔍 Access Modifier Comparison

| Modifier | Same Class | Child Class | Outside |
|---|---|---|---|
| `public` | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ❌ |
| `private` | ✅ | ❌ | ❌ |

সহজভাবে:

```text
public
   ↓
সব জায়গা

protected
   ↓
Class + Child Class

private
   ↓
শুধু নিজের Class
```

---

## 🔗 Laravel Connection

Laravel Model-এ Access Modifier খুব common।

```php
class User extends Model
{
    protected $fillable = [
        'name',
        'email',
    ];
}
```

এখানে `$fillable` একটি `protected` property।

আর Controller/Service-এ:

```php
class UserController extends Controller
{
    private UserService $userService;
}
```

`private` ব্যবহার করে internal dependency/property
বাইরে থেকে direct access করা বন্ধ রাখা যায়।

---

## ⚠️ Common Mistake

❌ `private` property বাইরে থেকে access:

```php
$user->password;
```

যদি property হয়:

```php
private string $password;
```

তাহলে এটি কাজ করবে না।

---

## 📝 Practice

### Exercise 01

`User` Class তৈরি করো:

```text
public $name
private $password
protected $role
```

প্রতিটি property কোথা থেকে access করা যায় test করো।

### Exercise 02

`Admin` Class তৈরি করে `User` থেকে inherit করো এবং
`protected $role` access করে দেখো।

---

## 📌 Quick Summary

```text
public
→ Everywhere

protected
→ Class + Child Class

private
→ Same Class Only
```

> 🎯 **Goal:** `public`, `protected` এবং `private` ভালোভাবে
> বুঝে Laravel-এর Model, Controller এবং Service-এর code
> সহজে বুঝতে পারা।