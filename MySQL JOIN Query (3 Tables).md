নিচে আমরা ৩টি টেবিল – `users`, `categories`, এবং `products` নিয়ে **MySQL-এর সব ধরনের JOIN** সম্পর্কে আলোচনা করবোঃ

---

## 📋 ধরি টেবিল ৩টি নিচের মতো:

### 🧍‍♂️ `users` টেবিল:

|id|user_name|
|---|---|
|1|Saiful|
|2|Jahid|
|3|Ishrak|
|4|Towsif|

---

### 📂 `categories` টেবিল:

|id|category_name|user_id|
|---|---|---|
|1|Electronics|1|
|2|Books|2|
|3|Clothing|NULL|
|4|Sports|5|

---

### 📦 `products` টেবিল:

| id  | product_name | category_id |
| --- | ------------ | ----------- |
| 1   | Laptop       | 1           |
| 2   | Quran Sharif | 2           |
| 3   | T-shirt      | 3           |
| 4   | Football     | 4           |
| 5   | Mouse        | NULL        |

---

## 🔶 1. INNER JOIN (3 টেবিল)

```sql
SELECT users.user_name, categories.category_name, products.product_name
FROM users
INNER JOIN categories ON users.id = categories.user_id
INNER JOIN products ON categories.id = products.category_id;
```

🟢 ফলাফল:

|user_name|category_name|product_name|
|---|---|---|
|Saiful|Electronics|Laptop|
|Jahid|Books|Quran Sharif|

---

## 🔷 2. LEFT JOIN (users → categories → products)

```sql
SELECT users.user_name, categories.category_name, products.product_name
FROM users
LEFT JOIN categories ON users.id = categories.user_id
LEFT JOIN products ON categories.id = products.category_id;
```

🟢 ফলাফল:

|user_name|category_name|product_name|
|---|---|---|
|Saiful|Electronics|Laptop|
|Jahid|Books|Quran Sharif|
|Ishrak|NULL|NULL|
|Towsif|NULL|NULL|

---

## 🔷 3. RIGHT JOIN (users ← categories ← products)

```sql
SELECT users.user_name, categories.category_name, products.product_name
FROM users
RIGHT JOIN categories ON users.id = categories.user_id
RIGHT JOIN products ON categories.id = products.category_id;
```

🟢 ফলাফল:

|user_name|category_name|product_name|
|---|---|---|
|Saiful|Electronics|Laptop|
|Jahid|Books|Quran Sharif|
|NULL|Clothing|T-shirt|
|NULL|Sports|Football|

---

## 🔶 4. FULL OUTER JOIN (LEFT + RIGHT)

```sql
-- FULL OUTER JOIN Simulation in MySQL
SELECT users.user_name, categories.category_name, products.product_name
FROM users
LEFT JOIN categories ON users.id = categories.user_id
LEFT JOIN products ON categories.id = products.category_id

UNION

SELECT users.user_name, categories.category_name, products.product_name
FROM users
RIGHT JOIN categories ON users.id = categories.user_id
RIGHT JOIN products ON categories.id = products.category_id
WHERE users.id IS NULL;
```

🟢 ফলাফল:

|user_name|category_name|product_name|
|---|---|---|
|Saiful|Electronics|Laptop|
|Jahid|Books|Quran Sharif|
|Ishrak|NULL|NULL|
|Towsif|NULL|NULL|
|NULL|Clothing|T-shirt|
|NULL|Sports|Football|

---

## 🔷 5. CROSS JOIN (সবচেয়ে বিপজ্জনক JOIN 😄)

```sql
SELECT users.user_name, categories.category_name, products.product_name
FROM users
CROSS JOIN categories
CROSS JOIN products;
```

🟢 ফলাফল:

- Total: 4 users × 4 categories × 5 products = **80 rows**
    
- উদাহরণ:  
    Saiful – Electronics – Laptop  
    Jahid – Books – Quran Sharif  
    ... (সবচেয়ে বিশৃঙ্খল)
    

---

## ✅ সারসংক্ষেপ (JOIN অনুযায়ী ফলাফল):

|JOIN টাইপ|ফলাফল কেমন|NULL Support|Matching|
|---|---|---|---|
|INNER JOIN|কেবল পুরোপুরি match|❌|users+categories+products|
|LEFT JOIN|সব users দেখায়|✅|যেটুকু match|
|RIGHT JOIN|সব products দেখায়|✅|যেটুকু match|
|FULL OUTER JOIN|সব টেবিলের সব রেকর্ড|✅|যেটুকু match|
|CROSS JOIN|সব combination|❌|No match needed|

---
