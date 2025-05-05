MySQL একটি জনপ্রিয় ওপেন সোর্স রিলেশনাল ডাটাবেস ম্যানেজমেন্ট সিস্টেম (RDBMS)। এটি SQL (Structured Query Language) ব্যবহার করে ডেটা পরিচালনা ও রক্ষা করে। MySQL সাধারণত ডেটাবেস অ্যাপ্লিকেশন তৈরি করতে ব্যবহৃত হয়, যেমন ওয়েব অ্যাপ্লিকেশন, ই-কমার্স সাইট, ব্লগ, এবং অন্যান্য সফটওয়্যার যেখানে ডেটা সঞ্চয়, পুনরুদ্ধার, আপডেট এবং ম্যানিপুলেশন প্রয়োজন।

# **Essential Commands and Example**


##  **1. SQL Command Categories**

| Category                              | Description                               | Commands                              |
| ------------------------------------- | ----------------------------------------- | ------------------------------------- |
| **DDL**(Data Definition Language)     | ডাটাবেসের কাঠামো তৈরি ও পরিবর্তনের জন্য   | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DQL**(Data Query Language)          | ডেটা অনুসন্ধানের জন্য                     | `SELECT`                              |
| **DML**(Data Manipulation Language)   | ডেটা যোগ, হালনাগাদ, মুছার জন্য            | `INSERT`, `UPDATE`, `DELETE`          |
| **DCL**(Data Control Language)        | ডেটাবেসে অনুমতি দেওয়া বা বাতিল করার জন্য | `GRANT`, `REVOKE`                     |
| **TCL**(Transaction Control Language) | ট্রানজেকশন নিয়ন্ত্রণের জন্য              | `COMMIT`, `ROLLBACK`, `SAVEPOINT`     |

---

##  **2. Common SQL Operators**

|Type|Operators|Usage Example|
|---|---|---|
|**Arithmetic**|`+`, `-`, `*`, `/`, `%`|`SELECT 10 + 5;` → `15`|
|**Comparison**|`=`, `!=`, `<`, `>`, `<=`, `>=`|`WHERE age >= 18`|
|**Logical**|`AND`, `OR`, `NOT`, `BETWEEN`, `IN`, `LIKE`|`WHERE name LIKE 'J%' AND age BETWEEN 20 AND 30`|

---

##  **3. Essential SQL Clauses**

|Clause|Description|Example|
|---|---|---|
|`WHERE`|ডেটা ফিল্টার করার জন্য|`SELECT * FROM users WHERE age > 18;`|
|`ORDER BY`|ফলাফল সর্ট করার জন্য|`SELECT * FROM users ORDER BY age DESC;`|
|`GROUP BY`|একাধিক রেকর্ডকে গ্রুপ করার জন্য|`SELECT dept, COUNT(*) FROM employees GROUP BY dept;`|
|`HAVING`|গ্রুপড ডেটা ফিল্টার করার জন্য|`HAVING COUNT(*) > 5`|

---

##  **4. Important Database Objects**

|**Object**|**Description**|**উদাহরণ (সংক্ষেপে)**|
|---|---|---|
|**TABLE**|ডেটা সংরক্ষণের জন্য কাঠামো|`CREATE TABLE Products (id INT, name VARCHAR(100));`|
|**VIEW**|একটি ভার্চুয়াল টেবিল যা কুয়েরি দিয়ে তৈরি|`CREATE VIEW ActiveProducts AS SELECT * FROM Products WHERE status = 'active';`|
|**INDEX**|ডেটা দ্রুত খুঁজে বের করতে সাহায্য করে|`CREATE INDEX idx_name ON Products(name);`|

---

##  **5. SQL Constraints (নিয়ম)**

|**Constraint**|**কাজ**|**উদাহরণ (সংক্ষেপে)**|
|---|---|---|
|`PRIMARY KEY`|প্রতিটি রেকর্ডকে ইউনিকভাবে চিহ্নিত করে|`id INT PRIMARY KEY`|
|`FOREIGN KEY`|দুটি টেবলের মধ্যে সম্পর্ক তৈরি করে|`category_id INT, FOREIGN KEY (category_id) REFERENCES Categories(id)`|
|`NOT NULL`|নিশ্চিত করে যে কোনো ফিল্ড খালি রাখা যাবে না|`name VARCHAR(100) NOT NULL`|
|`UNIQUE`|একটি কলামে প্রতিটি ভ্যালু ইউনিক হতে হবে|`email VARCHAR(100) UNIQUE`|
|`DEFAULT`|কোনো মান না দিলে স্বয়ংক্রিয়ভাবে একটি ডিফল্ট মান সেট করে|`status VARCHAR(10) DEFAULT 'active'`|
|`CHECK`|নির্দিষ্ট শর্ত পূরণ না করলে ডেটা ইনসার্ট করতে দেয় না|`age INT CHECK (age >= 18)`|

---

##  **6. Aggregation Functions (সারাংশ ফাংশন)**


|**Function**|**কাজ**|**উদাহরণ (সংক্ষেপে)**|
|---|---|---|
|`COUNT()`|কতগুলো রেকর্ড আছে তা গণনা করে|`SELECT COUNT(*) FROM Products;`|
|`SUM()`|একটি কলামের মোট যোগফল|`SELECT SUM(price) FROM Products;`|
|`AVG()`|গড় মান হিসাব করে|`SELECT AVG(price) FROM Products;`|
|`MAX()` / `MIN()`|সর্বোচ্চ / সর্বনিম্ন মান বের করে|`SELECT MAX(price), MIN(price) FROM Products;`|
|`COUNT()` (GROUP BY)|প্রতিটি গ্রুপের জন্য রেকর্ড গণনা করে|`SELECT category_id, COUNT(*) FROM Products GROUP BY category_id;`|
|`SUM()` (GROUP BY)|প্রতিটি গ্রুপের জন্য মোট যোগফল করে|`SELECT category_id, SUM(price) FROM Products GROUP BY category_id;`|
|`AVG()` (GROUP BY)|প্রতিটি গ্রুপের জন্য গড় মান বের করে|`SELECT category_id, AVG(price) FROM Products GROUP BY category_id;`|
|`MAX()` / `MIN()` (GROUP BY)|প্রতিটি গ্রুপের জন্য সর্বোচ্চ / সর্বনিম্ন মান বের করে|`SELECT category_id, MAX(price), MIN(price) FROM Products GROUP BY category_id;`|


---

##  **7. Joins (জয়েনস)**

|**Join Type**|**Description**|**উদাহরণ (সংক্ষেপে)**|
|---|---|---|
|INNER JOIN|দুই টেবলের মিলে যাওয়া রেকর্ডগুলো দেখায়|`SELECT * FROM Products INNER JOIN Categories ON Products.category_id = Categories.id;`|
|LEFT JOIN|বাম টেবলের সব রেকর্ড + ডান টেবলের মিলে যাওয়া রেকর্ড|`SELECT * FROM Products LEFT JOIN Categories ON Products.category_id = Categories.id;`|
|RIGHT JOIN|ডান টেবলের সব রেকর্ড + বাম টেবলের মিলে যাওয়া রেকর্ড|`SELECT * FROM Products RIGHT JOIN Categories ON Products.category_id = Categories.id;`|
|FULL JOIN|দুই টেবলের সব রেকর্ড দেখায় — যেখানে মিল আছে সেগুলো একসাথে, আর যেখানে মিল নেই সেখানে NULL দেখায়|`SELECT * FROM Products FULL JOIN Categories ON Products.category_id = Categories.id;`|

---

##  **8. Set Operations (সেট অপারেশন)**

নিচে তোমার দেওয়া টেবিলটি সংক্ষেপে উদাহরণসহ পূর্ণাঙ্গ করে দিলাম:

|**Operation**|**কাজ**|**উদাহরণ (সংক্ষেপে)**|
|---|---|---|
|`UNION`|দুই কুয়েরির ফলাফল একসাথে করে (ডুপ্লিকেট বাদ দিয়ে)|`SELECT name FROM Products UNION SELECT name FROM Categories;`|
|`INTERSECT`|দুই কুয়েরির সাধারণ রেকর্ড|`SELECT name FROM Products INTERSECT SELECT name FROM Categories;`|
|`EXCEPT`|প্রথম কুয়েরিতে আছে, কিন্তু দ্বিতীয়টিতে নেই এমন রেকর্ড|`SELECT name FROM Products EXCEPT SELECT name FROM Categories;`|

---