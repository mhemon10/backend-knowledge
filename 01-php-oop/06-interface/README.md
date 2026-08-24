# 🐘 06 | Interface

**Interface** হলো একটি contract, যেখানে কোনো Class-এ কোন
method থাকতে হবে তা define করা হয়।

Interface-এর method-এর সাধারণত implementation থাকে না।
যে Class `implements` করবে, তাকে সেই method implement করতে হবে।

---

## 🔹 Basic Example

```php
interface PaymentInterface
{
    public function pay(float $amount): string;
}

class StripePayment implements PaymentInterface
{
    public function pay(float $amount): string
    {
        return "Paid $amount using Stripe";
    }
}

$payment = new StripePayment();

echo $payment->pay(1000);
```

### Output

```text
Paid 1000 using Stripe
```

---

## 🔹 `implements`

Interface ব্যবহার করতে `implements` keyword ব্যবহার করা হয়।

```php
class StripePayment implements PaymentInterface
{
}
```

একটি Class একাধিক Interface implement করতে পারে:

```php
interface Loggable
{
    public function log(): void;
}

interface Payable
{
    public function pay(): void;
}

class PaymentService implements Loggable, Payable
{
    public function log(): void
    {
        echo "Payment logged";
    }

    public function pay(): void
    {
        echo "Payment completed";
    }
}
```

---

## 🔗 Laravel Connection

Laravel application-এ Interface সাধারণত
**Service / Repository architecture** এবং
**Dependency Injection**-এর সাথে ব্যবহার করা হয়।

```php
interface PaymentServiceInterface
{
    public function pay(float $amount): bool;
}
```

Implementation:

```php
class StripePaymentService implements PaymentServiceInterface
{
    public function pay(float $amount): bool
    {
        return true;
    }
}
```

তারপর Controller-এ Interface inject করা যায়:

```php
class PaymentController extends Controller
{
    public function __construct(
        private PaymentServiceInterface $paymentService
    ) {
    }
}
```

এখানে Controller জানে শুধু:

```text
PaymentServiceInterface
        ↓
      Contract
```

কোন implementation ব্যবহার হচ্ছে সেটা আলাদা রাখা যায়।

---

## 🔍 Interface vs Abstract Class

| Interface | Abstract Class |
|---|---|
| `interface` keyword | `abstract class` |
| `implements` | `extends` |
| Contract define করে | Base functionality দিতে পারে |
| একাধিক Interface implement করা যায় | একটি parent class extend করা যায় |
| সাধারণত method contract থাকে | Abstract + normal method থাকতে পারে |

---

## ⚠️ Common Mistake

Interface-এ:

```php
interface PaymentInterface
{
    public function pay(): string;
}
```

কিন্তু Class-এ method implement না করলে error হবে:

```php
class StripePayment implements PaymentInterface
{
}
```

সঠিক:

```php
class StripePayment implements PaymentInterface
{
    public function pay(): string
    {
        return "Payment successful";
    }
}
```

---

## 📝 Practice

### Exercise 01

একটি `PaymentInterface` তৈরি করো:

```php
pay(float $amount)
```

তারপর:

```text
StripePayment
SSLCommerzPayment
```

দুটি Class দিয়ে implement করো।

### Exercise 02

একটি `NotificationInterface` তৈরি করো:

```php
send(string $message)
```

তারপর:

```text
EmailNotification
SmsNotification
```

দুটি implementation তৈরি করো।

---

## 📌 Quick Summary

```text
Interface
    ↓
Contract
    ↓
implements
    ↓
Class
    ↓
Method Implementation
```

- `interface` → Contract তৈরি করে
- `implements` → Interface ব্যবহার করে
- Interface-এর required method implement করতে হয়
- একটি Class একাধিক Interface implement করতে পারে
- Laravel-এ Interface + Dependency Injection খুব useful

> 🎯 **Goal:** Interface বুঝে Laravel-এর Service,
> Repository এবং Dependency Injection architecture বুঝতে পারা।