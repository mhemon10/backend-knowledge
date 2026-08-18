# PHP OOP Concepts

## 1. Class

Class হলো object তৈরি করার blueprint।

Example:

class User
{
    public string $name;
}

---

## 2. Object

Class থেকে তৈরি হওয়া instance হলো Object।

$user = new User();

---

## 3. Inheritance

একটি class অন্য class-এর properties এবং methods inherit করতে পারে।

class Admin extends User

---

## 4. Encapsulation

Data এবং behavior একই class-এর মধ্যে রাখা এবং
access control করা।

---

## 5. Abstraction

Complex implementation hide করে শুধু প্রয়োজনীয়
interface expose করা।

---

## 6. Polymorphism

একই interface/method বিভিন্ন class-এ
ভিন্নভাবে কাজ করতে পারে।

---

## 7. Interface

একটি class কী কী method implement করবে তার contract।

---

## 8. Trait

একাধিক unrelated class-এর মধ্যে reusable methods
share করার জন্য ব্যবহার করা হয়।