# 🗄️ 07 | Auto Commit & Transactions

Database-এ কোনো query execute করার পর changes কীভাবে
save বা undo হবে, সেটার সাথে **Auto Commit** এবং
**Transaction** সম্পর্কিত।

---

## 🔹 Auto Commit

MySQL-এ **Auto Commit enabled** থাকলে প্রতিটি
successful SQL statement automatically database-এ
save হয়ে যায়।

Check করতে:

```sql
SELECT @@autocommit;
```

### Output

```text
1
```

```text
1 → Auto Commit ON
0 → Auto Commit OFF
```

---

## 🔹 Disable Auto Commit

```sql
SET autocommit = 0;
```

এখন changes automatically commit হবে না।

---

## 🔹 Commit

Changes permanently save করতে:

```sql
COMMIT;
```

---

## 🔹 Rollback

Uncommitted changes undo করতে:

```sql
ROLLBACK;
```

---

# 🔄 Transactions

**Transaction** হলো একাধিক SQL operation-কে একটি
single unit হিসেবে execute করার process।

```text
START TRANSACTION
       ↓
   Query 1
       ↓
   Query 2
       ↓
     COMMIT
       ↓
    Success
```

কোনো সমস্যা হলে:

```text
START TRANSACTION
       ↓
   Query 1
       ↓
   Query 2 ❌
       ↓
   ROLLBACK
       ↓
 Changes Undo
```

---

## 🔹 Basic Transaction

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

দুটি operation সফল হলে `COMMIT` করে changes save হবে।

---

## 🔹 Rollback Example

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

ROLLBACK;
```

`ROLLBACK` করলে transaction-এর ভিতরের changes undo হবে।

---

## 🔗 Laravel Connection

Laravel-এ Database Transaction করার জন্য:

```php
DB::transaction(function () {

    Account::find(1)
        ->decrement('balance', 1000);

    Account::find(2)
        ->increment('balance', 1000);

});
```

Laravel automatically:

```text
Success
   ↓
COMMIT

Error
   ↓
ROLLBACK
```

---

## 💡 Real World Example

Bank money transfer-এর ক্ষেত্রে:

```text
Account A
   ↓
- 1000

Account B
   ↓
+ 1000
```

দ্বিতীয় operation fail করলে প্রথম operation-ও
rollback হওয়া দরকার।

এজন্য Transaction ব্যবহার করা হয়।

---

## 📌 Quick Summary

| Command | কাজ |
|---|---|
| `START TRANSACTION` | Transaction শুরু |
| `COMMIT` | Changes permanently save |
| `ROLLBACK` | Changes undo |
| `SET autocommit = 0` | Auto Commit বন্ধ |

```text
Transaction
     ↓
Multiple Queries
     ↓
All Success → COMMIT
Any Failure → ROLLBACK
```

> 🎯 **Goal:** MySQL Transaction বুঝে Laravel-এ
> `DB::transaction()` safely ব্যবহার করতে পারা।