# 🐘 01 | Class & Object

Object-Oriented Programming (OOP)-এর সবচেয়ে fundamental
concept হলো **Class** এবং **Object**।

PHP-তে OOP শেখার সময় প্রথমেই Class এবং Object ভালোভাবে
বোঝা গুরুত্বপূর্ণ, কারণ Laravel-এর Model, Controller,
Service সহ প্রায় সবকিছুই PHP Class-এর উপর ভিত্তি করে তৈরি।

---

## 📚 এই অধ্যায়ে যা শিখব

1. Class কী?
2. Object কী?
3. Class এবং Object-এর মধ্যে পার্থক্য
4. Property কী?
5. Method কী?
6. Object কীভাবে তৈরি করতে হয়
7. Property কীভাবে access করতে হয়
8. Method কীভাবে call করতে হয়
9. Real-world example
10. Laravel-এর সাথে connection
11. Common mistakes
12. Practice

---

# 🔹 Class কী?

**Class হলো Object তৈরি করার একটি blueprint বা template।**

একটি Class-এর মধ্যে সাধারণত দুই ধরনের জিনিস থাকে:

- **Properties** → Object-এর data/state
- **Methods** → Object-এর behavior/action

সহজভাবে:

```text
Class
│
├── Properties
│   ├── name
│   ├── email
│   └── age
│
└── Methods
    ├── login()
    ├── logout()
    └── updateProfile()
```

---

## 🔹 Basic Class

PHP-তে একটি Class তৈরি করতে `class` keyword ব্যবহার করা হয়।

```php
class User
{
}
```

এখানে `User` হলো একটি Class।

তবে এই Class-এর মধ্যে এখনো কোনো property বা method নেই।

---

# 🔹 Object কী?

**Object হলো কোনো Class-এর একটি instance।**

অর্থাৎ Class হলো blueprint এবং Object হলো সেই blueprint
থেকে তৈরি হওয়া বাস্তব instance।

```text
Class
  ↓
Blueprint

Object
  ↓
Class থেকে তৈরি Instance
```

PHP-তে Object তৈরি করতে `new` keyword ব্যবহার করা হয়।

```php
class User
{
}

$user = new User();
```

এখানে:

```text
User
 ↓
Class

new User()
 ↓
Object তৈরি

$user
 ↓
Object
```

---

# 🔹 Class এবং Object-এর সম্পর্ক

ধরো, আমাদের একটি `User` Class আছে।

```php
class User
{
}
```

এই Class থেকে আমরা অনেকগুলো Object তৈরি করতে পারি।

```php
$user1 = new User();
$user2 = new User();
$user3 = new User();
```

তাহলে:

```text
             User Class
                 │
        ┌────────┼────────┐
        ↓        ↓        ↓
     $user1    $user2    $user3
     Object    Object    Object
```

সবগুলো Object একই `User` Class-এর instance।

---

# 🔹 Property কী?

Class-এর ভিতরে থাকা variable-কে **Property** বলা হয়।

Example:

```php
class User
{
    public string $name;
    public string $email;
}
```

এখানে:

```text
$name
$email
```

দুটোই `User` Class-এর Property।

---

## 🔹 Property ব্যবহার

প্রথমে Object তৈরি করতে হবে:

```php
$user = new User();
```

তারপর Object-এর মাধ্যমে Property-তে value assign করা যায়।

```php
$user->name = "Emon";
$user->email = "emon@example.com";
```

Value read করাও যায়:

```php
echo $user->name;
echo $user->email;
```

### Output

```text
Emon
emon@example.com
```

---

# 🔹 Complete Property Example

```php
class User
{
    public string $name;
    public string $email;
}

$user = new User();

$user->name = "Emon";
$user->email = "emon@example.com";

echo $user->name;
echo "\n";
echo $user->email;
```

### Output

```text
Emon
emon@example.com
```

---

# 🔹 Method কী?

Class-এর ভিতরে থাকা function-কে **Method** বলা হয়।

Example:

```php
class User
{
    public function login(): string
    {
        return "User logged in";
    }
}
```

এখানে:

```text
login()
 ↓
Method
```

---

## 🔹 Method Call করা

প্রথমে Object তৈরি করতে হবে:

```php
$user = new User();
```

তারপর Object-এর মাধ্যমে method call করতে হবে:

```php
echo $user->login();
```

### Output

```text
User logged in
```

---

# 🔹 Property + Method একসাথে

একটি Class-এর মধ্যে Property এবং Method দুটোই থাকতে পারে।

```php
class User
{
    public string $name;

    public function login(): string
    {
        return $this->name . " logged in";
    }
}

$user = new User();

$user->name = "Emon";

echo $user->login();
```

### Output

```text
Emon logged in
```

---

# 🔍 এখানে `$this` কী?

`$this` হলো **বর্তমান Object-এর reference**।

উপরের example-এ:

```php
return $this->name . " logged in";
```

`$this->name` বলতে বোঝাচ্ছে:

> এই Object-এর `name` Property।

Example:

```php
$user->name = "Emon";
```

তারপর:

```php
$user->login();
```

তখন `$this` হলো `$user` Object।

```text
$user
  │
  ├── name = "Emon"
  │
  └── login()
        ↓
      $this
        ↓
   $user Object
```

---

# 🔹 Real World Example

ধরো আমরা একটি e-commerce application তৈরি করছি।

আমাদের একজন User-এর কিছু information থাকবে:

```text
User
│
├── name
├── email
├── phone
│
├── login()
├── logout()
└── updateProfile()
```

এটা PHP-তে:

```php
class User
{
    public string $name;
    public string $email;
    public string $phone;

    public function login(): string
    {
        return $this->name . " logged in";
    }

    public function logout(): string
    {
        return $this->name . " logged out";
    }

    public function updateProfile(): string
    {
        return $this->name . " profile updated";
    }
}
```

Object তৈরি:

```php
$user = new User();

$user->name = "Emon";
$user->email = "emon@example.com";
$user->phone = "01700000000";

echo $user->login();
echo "\n";

echo $user->updateProfile();
echo "\n";

echo $user->logout();
```

### Output

```text
Emon logged in
Emon profile updated
Emon logged out
```

---

# 🔹 Multiple Objects

একই Class থেকে আমরা multiple Object তৈরি করতে পারি।

```php
class User
{
    public string $name;

    public function login(): string
    {
        return $this->name . " logged in";
    }
}

$user1 = new User();
$user1->name = "Emon";

$user2 = new User();
$user2->name = "Sakil";

echo $user1->login();
echo "\n";

echo $user2->login();
```

### Output

```text
Emon logged in
Sakil logged in
```

এখানে `user1` এবং `user2` একই Class-এর Object হলেও
তাদের data আলাদা।

```text
             User Class
                 │
        ┌────────┴────────┐
        ↓                 ↓
     $user1             $user2
        │                 │
   name = Emon       name = Sakil
```

---

# 🔹 Class vs Object

| বিষয় | Class | Object |
|---|---|---|
| কী? | Blueprint | Instance |
| তৈরি করতে | `class` | `new` |
| Data | Define করে | Store করে |
| Method | Define করে | ব্যবহার করে |
| Example | `User` | `$user` |

সহজভাবে মনে রাখো:

```text
Class  = Blueprint
Object = Blueprint থেকে তৈরি বাস্তব Instance
```

---

# 🔗 Laravel-এর সাথে Connection

Laravel-এর ভিতরে PHP OOP-এর Class & Object concept
প্রতিনিয়ত ব্যবহার করা হয়।

---

## 🔹 Laravel Model

Laravel-এর একটি সাধারণ Model:

```php
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
}
```

এখানে `User` একটি PHP Class।

```text
User
 ↓
Class
```

এবং এটি Laravel-এর `Model` Class থেকে inherit করছে।

```text
User
 ↓
extends
 ↓
Model
```

---

## 🔹 Laravel Model থেকে Object

আমরা Model-এর Object তৈরি করতে পারি:

```php
$user = new User();

$user->name = "Emon";

$user->save();
```

এখানে:

```text
new User()
    ↓
User Model Object
    ↓
Database
```

---

## 🔹 Laravel Controller

Laravel Controller-ও একটি PHP Class।

```php
namespace App\Http\Controllers;

class UserController extends Controller
{
    public function index()
    {
        return "Users";
    }
}
```

এখানে:

```text
UserController
      ↓
    Class
```

`index()` হলো একটি Method।

---

## 🔹 Laravel Service

Real-world Laravel application-এ আমরা Service Class
ব্যবহার করতে পারি।

```php
class UserService
{
    public function getUsers()
    {
        return User::all();
    }
}
```

এখানেও:

```text
UserService
     ↓
   Class

getUsers()
     ↓
   Method
```

---

# 🧠 PHP OOP → Laravel Map

```text
PHP OOP
   │
   ├── Class
   │      ↓
   │   Laravel Model
   │   Laravel Controller
   │   Laravel Service
   │
   ├── Object
   │      ↓
   │   Model Object
   │   Service Object
   │
   └── Method
          ↓
      Controller Method
      Service Method
      Model Method
```

---

# ⚠️ Common Mistakes

## ❌ Mistake 01 — `new` ছাড়া Object তৈরি করা

ভুল:

```php
$user = User();
```

সঠিক:

```php
$user = new User();
```

Object তৈরি করার জন্য `new` keyword ব্যবহার করতে হয়।

---

## ❌ Mistake 02 — Property access করার সময় `->` ব্যবহার না করা

ভুল:

```php
$user.name;
```

সঠিক:

```php
$user->name;
```

PHP Object-এর property এবং method access করতে `->`
operator ব্যবহার করা হয়।

---

## ❌ Mistake 03 — Method call করার সময় `()` না দেওয়া

ভুল:

```php
$user->login;
```

সঠিক:

```php
$user->login();
```

কারণ `login()` একটি method।

---

# 📝 Practice

## Exercise 01 — User Class

একটি `User` Class তৈরি করো।

Properties:

```text
$name
$email
$phone
```

Methods:

```text
login()
logout()
getProfile()
```

তারপর একটি Object তৈরি করে সবগুলো ব্যবহার করো।

---

## Exercise 02 — Product Class

একটি `Product` Class তৈরি করো।

Properties:

```text
$name
$price
$category
```

Methods:

```text
getPrice()
getDetails()
```

Example:

```php
$product = new Product();

$product->name = "Laptop";
$product->price = 80000;
$product->category = "Electronics";
```

Expected output:

```text
Product: Laptop
Price: 80000
Category: Electronics
```

---

## Exercise 03 — Multiple Objects

একটি `Student` Class তৈরি করো।

Properties:

```text
$name
$age
$department
```

তারপর তিনটি Object তৈরি করো:

```text
Student 1 → Emon
Student 2 → Sakil
Student 3 → Rahim
```

প্রতিটি Student-এর information print করো।

---

# 🚀 Laravel Practice

Laravel-এ একটি `User` Model তৈরি করো:

```php
class User extends Model
{
}
```

তারপর Object তৈরি করো:

```php
$user = new User();

$user->name = "Emon";
$user->email = "emon@example.com";

$user->save();
```

তারপর database থেকে User retrieve করো:

```php
$user = User::find(1);

echo $user->name;
```

এখানে PHP-এর Class & Object concept কীভাবে
Laravel Eloquent-এর সাথে কাজ করছে সেটা লক্ষ্য করো।

---

# 📌 Quick Summary

```text
Class
 ↓
Object তৈরির Blueprint

Object
 ↓
Class-এর Instance

Property
 ↓
Object-এর Data / State

Method
 ↓
Object-এর Behavior

new
 ↓
Object তৈরি করার Keyword

$this
 ↓
Current Object-এর Reference
```

---

# 🎯 Key Takeaways

- Class হলো Object-এর blueprint।
- Object হলো Class-এর instance।
- `new` keyword দিয়ে Object তৈরি করা হয়।
- Class-এর ভিতরে Property এবং Method থাকতে পারে।
- Property Object-এর data/state represent করে।
- Method Object-এর behavior/action represent করে।
- Object-এর property access করতে `->` ব্যবহার করা হয়।
- Object-এর method call করতেও `->` ব্যবহার করা হয়।
- `$this` current Object-কে refer করে।
- Laravel-এর Model, Controller এবং Service PHP Class-এর
  উপর ভিত্তি করে তৈরি।
- PHP Class & Object ভালোভাবে বুঝলে Laravel-এর structure
  বোঝা অনেক সহজ হয়।

---

> 🎯 **Goal:** Class এবং Object-এর concept এমনভাবে বোঝা,
> যাতে Laravel-এর Model, Controller এবং Service দেখলে
> এগুলোর OOP structure সহজেই বুঝতে পারি।