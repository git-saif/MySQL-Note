
## 🧾 JOIN কি?

JOIN ব্যবহার করা হয় একাধিক টেবিল থেকে সম্পর্কযুক্ত ডেটা একত্রে আনার জন্য।  
JOIN মূলত `ON` বা `USING` শর্ত দিয়ে নির্দিষ্ট কলামের ভিত্তিতে ডেটা মিলিয়ে ফলাফল দেখায়।

---

## 🧭 LEFT TABLE ও RIGHT TABLE কীভাবে বুঝবো?

JOIN-এর কাঠামো:

```sql
SELECT ...
FROM table1
LEFT|RIGHT JOIN table2 ON ...
```

- `FROM table1` → এটিই **LEFT TABLE**
    
- `JOIN table2` → এটিই **RIGHT TABLE**
    

👉 মানে JOIN টাইপ যেটাই হোক না কেন, `FROM`-এর পর পরই যেটা আছে তা **LEFT**, আর JOIN-এর পরে যেটা আছে তা **RIGHT**।

---

## 🧾 ধরি দুইটি টেবিল:

### `users` টেবিল:

| id  | user_name |
| --- | --------- |
| 1   | Alice     |
| 2   | Bob       |
| 3   | Charlie   |

### `categories` টেবিল:

|id|category_name|user_id|
|---|---|---|
|1|Electronics|1|
|2|Books|2|
|3|Clothing|NULL|
|4|Sports|4|

> ⚠️ `categories.user_id` হচ্ছে `users.id` এর foreign key

---

## 🔶 1. INNER JOIN

👉 দুই টেবিলেই যেসব রেকর্ড মেলে, শুধু সেগুলোই দেখায়।

```sql
SELECT users.user_name, categories.category_name
FROM users
INNER JOIN categories ON users.id = categories.user_id;
```

🟢 ফলাফল:

| user_name | category_name |
| --------- | ------------- |
| Alice     | Electronics   |
| Bob       | Books         |


---

## 🔷 2. LEFT JOIN

👉 `users` টেবিলের সব রেকর্ড, আর `categories` টেবিল থেকে মিল পাওয়া ডেটা।

```sql
SELECT users.user_name, categories.category_name
FROM users
LEFT JOIN categories ON users.id = categories.user_id;
```

🟢 ফলাফল:

| user_name | category_name |
| --------- | ------------- |
| Alice     | Electronics   |
| Bob       | Books         |
| Charlie   | NULL          |



---

## 🔷 3. RIGHT JOIN

👉 `categories` টেবিলের সব রেকর্ড, আর `users` থেকে মিল পাওয়া ডেটা।

```sql
SELECT users.user_name, categories.category_name
FROM users
RIGHT JOIN categories ON users.id = categories.user_id;
```

🟢 ফলাফল:

| user_name | category_name |
| --------- | ------------- |
| Alice     | Electronics   |
| Bob       | Books         |
| NULL      | Clothing      |
| NULL      | Sports        |

---

## 🔶 4. FULL JOIN (MySQL-এ সরাসরি নেই, UNION দিয়ে করতে হয়)

👉 দুই টেবিলের সব রেকর্ড দেখায়, মিল থাকুক বা না থাকুক।

```sql
SELECT users.user_name, categories.category_name
FROM users
LEFT JOIN categories ON users.id = categories.user_id

UNION

SELECT users.user_name, categories.category_name
FROM users
RIGHT JOIN categories ON users.id = categories.user_id;
```

🟢 ফলাফল:

| user_name | category_name |
| --------- | ------------- |
| Alice     | Electronics   |
| Bob       | Books         |
| Charlie   | NULL          |
| NULL      | Clothing      |
| NULL      | Sports        |

---

## 🔷 5. CROSS JOIN

👉 প্রতিটি user এর সাথে প্রতিটি category জোড়া লাগানো (Cartesian Product)

```sql
SELECT users.user_name, categories.category_name
FROM users
CROSS JOIN categories;
```

🟢 ফলাফল: 3 users × 4 categories = 12 rows (Alice-Electronics, Alice-Books, ..., Charlie-Sports)

---

## 🔶 6. SELF JOIN (Bonus Example)

👉 ধরুন, `users` টেবিলে একজন ইউজার অন্য একজন ইউজারকে রিপোর্ট করে, `users.reported_by` আছে।

```sql
SELECT u1.user_name AS User, u2.user_name AS ReportedBy
FROM users u1
LEFT JOIN users u2 ON u1.reported_by = u2.id;
```

---

## 📌 সারসংক্ষেপ টেবিল:

|JOIN টাইপ|ফলাফল|
|---|---|
|**INNER JOIN**|কেবল মিল থাকা রেকর্ড|
|**LEFT JOIN**|সব users + মিল থাকা category|
|**RIGHT JOIN**|সব categories + মিল থাকা user|
|**FULL JOIN**|সব users + সব categories|
|**CROSS JOIN**|প্রতিটি user × প্রতিটি category|
|**SELF JOIN**|ইউজার নিজের টেবিলেই সম্পর্কযুক্ত|

---

## 📋 JOIN Quick Summary Table:

|JOIN টাইপ|LEFT TABLE|RIGHT TABLE|দেখায় কি?|
|---|---|---|---|
|**INNER JOIN**|FROM table|JOIN table|দুই দিকেই মিল|
|**LEFT JOIN**|FROM table|JOIN table|বাম দিকের সব|
|**RIGHT JOIN**|FROM table|JOIN table|ডান দিকের সব|
|**FULL JOIN**|FROM + JOIN|উভয়ই|দুই দিকের সব|
|**CROSS JOIN**|FROM table|JOIN table|সব কম্বিনেশন|
|**SELF JOIN**|এক টেবিল (দুই alias)|এক টেবিল (দুই alias)|নিজের সাথে সম্পর্ক|

---

## 🧠 মনে রাখার টিপস:

- **FROM-এর পরের টেবিল সবসময় LEFT**
    
- **JOIN-এর পরের টেবিল সবসময় RIGHT**
    
- **INNER JOIN** = LEFT + RIGHT টেবিলের যে ডেটা মিল পাওয়া যায় ।
    
- **LEFT JOIN** = LEFT টেবিলের সব ডেটা + RIGHT টেবিলের মিল পাওয়া ডেটা ।
    
- **RIGHT JOIN** = RIGHT টেবিলের সব ডেটা + LEFT টেবিলের মিল পাওয়া ডেটা ।

---
