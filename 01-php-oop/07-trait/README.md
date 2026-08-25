# 🐘 07 | Traits in PHP

**Trait** হলো PHP-এর একটি mechanism, যার মাধ্যমে একই
functionality একাধিক Class-এর মধ্যে reuse করা যায়।

Trait-এর জন্য `trait` এবং `use` keyword ব্যবহার করা হয়।

---

## 🔹 Basic Example

```php
trait Logger
{
    public function log(string $message): void
    {
        echo $message;
    }
}

class User
{
    use Logger;
}

$user = new User();

$user->log("User created");
```

### Output

```text
User created
```

এখানে `User` Class সরাসরি `Logger` Trait-এর method
ব্যবহার করতে পারছে।

---

## 🔹 Multiple Classes-এ Trait ব্যবহার

একই Trait একাধিক Class-এ ব্যবহার করা যায়।

```php
trait Logger
{
    public function log(string $message): void
    {
        echo $message;
    }
}

class User
{
    use Logger;
}

class Order
{
    use Logger;
}

$user = new User();
$order = new Order();

$user->log("User created");
$order->log("Order created");
```

### Output

```text
User created
Order created
```

---

## 🔗 Laravel Connection

Laravel-এ Trait খুব common।

### `HasFactory`

```php
use Illuminate\Database\Eloquent\Factories\HasFactory;

class User extends Model
{
    use HasFactory;
}
```

`HasFactory` Trait-এর functionality `User` Model-এ
available হয়ে যায়।

---

### `Notifiable`

Laravel-এর User Model-এ:

```php
use Illuminate\Notifications\Notifiable;

class User extends Model
{
    use Notifiable;
}
```

এখানে `Notifiable` Trait ব্যবহার করে notification-related
functionality পাওয়া যায়।

---

## 🔍 Trait vs Inheritance

| Trait | Inheritance |
|---|---|
| `trait` দিয়ে তৈরি | `class` দিয়ে তৈরি |
| `use` দিয়ে ব্যবহার | `extends` দিয়ে inherit |
| Code reuse-এর জন্য | Parent-child relationship |
| Multiple Trait ব্যবহার করা যায় | একটি parent class extend করা যায় |

---

## ⚠️ Common Mistake

Trait তৈরি করলেই Class-এ automatically পাওয়া যায় না।

❌ ভুল:

```php
class User
{
}
```

সঠিক:

```php
class User
{
    use Logger;
}
```

---

## 📝 Practice

### Exercise 01

একটি `Logger` Trait তৈরি করো:

```php
log(string $message)
```

তারপর `User` এবং `Order` Class-এ ব্যবহার করো।

### Exercise 02

একটি `Timestamp` Trait তৈরি করো:

```php
createdAt()
updatedAt()
```

তারপর একাধিক Class-এ reuse করো।

---

## 📌 Quick Summary

```text
Trait
  ↓
Reusable Functionality
  ↓
use
  ↓
Class
```

- `trait` → Reusable code তৈরি করে
- `use` → Class-এর মধ্যে Trait ব্যবহার করে
- একই Trait একাধিক Class-এ ব্যবহার করা যায়
- Laravel-এ `HasFactory`, `Notifiable` ইত্যাদি Trait-এর example

> 🎯 **Goal:** Trait বুঝে Laravel-এর reusable functionality
> এবং Model-এর `use HasFactory`, `use Notifiable` code
> সহজে বুঝতে পারা।