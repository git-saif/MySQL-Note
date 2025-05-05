

### 🧾 TCL কী?

**TCL (Transaction Control Language)** — যা **Transaction** পরিচালনা ও নিয়ন্ত্রণের জন্য ব্যবহৃত হয়। এটি ব্যবহার করা হয় যখন একাধিক SQL অপারেশন **একসাথে (transaction হিসেবে)** চালাতে হয়, যাতে সবগুলো সফল হলে একসাথে কমিট হয়, আর কোনো একটিতে সমস্যা হলে পুরো ট্রান্সঅ্যাকশন **rollback** হয়ে যায়।

---

### 🔹 প্রধান কমান্ড:

|Command|কাজ|
|---|---|
|`COMMIT`|ট্রান্সঅ্যাকশন সফলভাবে সম্পন্ন করে স্থায়ী করে|
|`ROLLBACK`|কোনো ভুল হলে আগের অবস্থায় ফিরে যায়|
|`SAVEPOINT`|ট্রান্সঅ্যাকশনের মাঝে একটি চেকপয়েন্ট তৈরি করে|
|`SET TRANSACTION`|ট্রান্সঅ্যাকশনের আলাদা বৈশিষ্ট্য নির্ধারণ করে (কম ব্যবহৃত)|

---

## ✅ বাস্তব উদাহরণ: E-commerce Context

ধরি আমরা দুটি টেবিলে কাজ করছি:  
🛒 `orders` এবং `payments`

```sql
START TRANSACTION;

-- 1. নতুন অর্ডার যোগ করো
INSERT INTO orders (customer_id, product_id, quantity) VALUES (1, 101, 2);

-- 2. পেমেন্ট এন্ট্রি করো
INSERT INTO payments (order_id, amount, status) VALUES (LAST_INSERT_ID(), 3000, 'pending');

-- যদি সবকিছু ঠিক থাকে, তাহলে কমিট করো
COMMIT;
```

🔸 এই `COMMIT` দিলে পুরো ট্রান্সঅ্যাকশন স্থায়ী হবে।

---

### ❌ যদি কোনো ভুল হয়, তাহলে:

```sql
START TRANSACTION;

-- অর্ডার ঢুকানো
INSERT INTO orders (customer_id, product_id, quantity) VALUES (2, 202, 1);

-- ভুল payment query
INSERT INTO payments (order_id, amount, status) VALUES (9999, 3000, 'pending'); -- ভুল order_id

-- সমস্যা বুঝে রোলব্যাক
ROLLBACK;
```

🔸 পুরো ট্রান্সঅ্যাকশন বাতিল হবে, কোনো ডেটাই থাকবে না।

---

### 📍 SAVEPOINT ব্যবহার:

```sql
START TRANSACTION;

INSERT INTO orders (customer_id, product_id, quantity) VALUES (3, 301, 1);
SAVEPOINT after_order;

INSERT INTO payments (order_id, amount, status) VALUES (LAST_INSERT_ID(), 5000, 'failed');

-- যদি payment সমস্যা করে
ROLLBACK TO after_order;

-- এরপর ঠিক থাকলে
COMMIT;
```

🔸 `SAVEPOINT` দিয়ে তুমি আংশিক rollback করতে পারো — পুরোটাই না।

---

## 📌 সংক্ষেপে TCL:

|Command|কাজ|
|---|---|
|`START TRANSACTION`|ট্রান্সঅ্যাকশন শুরু করে|
|`COMMIT`|পরিবর্তন স্থায়ী করে|
|`ROLLBACK`|সব পরিবর্তন বাতিল করে|
|`SAVEPOINT`|মাঝপথে ফিরে যাওয়ার পয়েন্ট|
|`ROLLBACK TO SAVEPOINT`|নির্দিষ্ট পয়েন্ট পর্যন্ত ফিরে যায়|

---

এই জিনিসগুলো মূলত তখনই কাজে লাগে যখন ডেটাবেজে **multiple steps** এ কাজ করতে হয়। যেমনঃ order → payment → stock update — যাতে সব একসাথে সফল হয় অথবা সব বাতিল হয়।

