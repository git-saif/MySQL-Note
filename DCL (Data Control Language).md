**DCL (Data Control Language)** SQL-এর একটি অংশ যা ডেটাবেজে **user access control** বা **permission** ম্যানেজ করার জন্য ব্যবহৃত হয়।

---

## 🔐 **DCL (Data Control Language)**

### 🔹 প্রধান কমান্ড:

|Command|কাজ|
|---|---|
|`GRANT`|ব্যবহারকারীর কোনো নির্দিষ্ট অনুমতি দেওয়া|
|`REVOKE`|ব্যবহারকারীর কাছ থেকে নির্দিষ্ট অনুমতি কেড়ে নেওয়া|

---

## ✅ **GRANT** – অনুমতি দেওয়া

ধরা যাক, একটি ব্যবহারকারী `shop_user` তৈরি করা হয়েছে এবং তাকে `products` টেবিল থেকে ডেটা দেখার অনুমতি দিতে চাই। তাহলেঃ

```sql
GRANT SELECT ON ecommerce_db.products TO 'shop_user'@'localhost';
```

🔸 অর্থ: `shop_user` এখন `products` টেবিল থেকে ডেটা দেখতে পারবে (SELECT পারমিশন)।

আরও উদাহরণ:

```sql
GRANT SELECT, INSERT, UPDATE ON ecommerce_db.* TO 'shop_user'@'localhost';
```

🔸 অর্থ: `shop_user` এখন `ecommerce_db` ডাটাবেসের সব টেবিলে SELECT, INSERT এবং UPDATE করতে পারবে।

---

## ❌ **REVOKE** – অনুমতি বাতিল

```sql
REVOKE INSERT, UPDATE ON ecommerce_db.products FROM 'shop_user'@'localhost';
```

🔸 অর্থ: `shop_user` আর `products` টেবিলে INSERT এবং UPDATE করতে পারবে না।

---

## 👥 Bonus: ইউজার তৈরি ও পাসওয়ার্ড দেওয়া

```sql
CREATE USER 'shop_user'@'localhost' IDENTIFIED BY 'securepassword';
```

---

## 📌 সংক্ষেপে DCL:

|Command|কাজ|উদাহরণ|
|---|---|---|
|`GRANT`|পারমিশন দেওয়া|`GRANT SELECT ON products TO 'user';`|
|`REVOKE`|পারমিশন কেড়ে নেওয়া|`REVOKE SELECT ON products FROM 'user';`|

---

🔒 DCL মূলত ডাটাবেজের নিরাপত্তা এবং ইউজার নিয়ন্ত্রণে ব্যবহৃত হয়। এটি বড় অ্যাপ্লিকেশন বা কোম্পানির ডেটাবেস ম্যানেজমেন্টে খুব গুরুত্বপূর্ণ।
