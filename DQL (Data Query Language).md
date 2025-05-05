
DQL মূলত ডেটাবেস থেকে ডেটা **query** বা **খোঁজার** জন্য ব্যবহৃত হয়। এর একমাত্র প্রধান কমান্ড হলো:

| Keyword    | কাজ                      |
| ---------- | ------------------------ |
| `SELECT`   | ডেটা নির্বাচন করা        |
| `FROM`     | কোন টেবিল থেকে ডেটা আনবে |
| `WHERE`    | শর্ত দেওয়া               |
| `ORDER BY` | সাজানো (ASC বা DESC)     |
| `JOIN`     | একাধিক টেবিল যুক্ত করা   |

নিচে এগুলোর বিস্তারিত বর্ণনা করা হলোঃ

> ✅ **`SELECT`** – টেবিল থেকে তথ্য বের করতে ব্যবহৃত হয়।

---

###  উদাহরণস্বরূপ ধরে নেই আমাদের দুটি টেবিল আছে:

#### 🗂️ **categories** টেবিল:

|id|name|
|---|---|
|1|Electronics|
|2|Clothing|

#### 📦 **products** টেবিল:

|id|name|category_id|price|
|---|---|---|---|
|1|Mobile Phone|1|15000|
|2|T-Shirt|2|500|
|3|Laptop|1|60000|
|4|Jeans|2|1200|

---

### উদাহরণ সহ DQL (`SELECT`, `FROM`, `WHERE`, `ORDER BY`, `JOIN`):

#### 1. 📋 সব প্রোডাক্ট লিস্ট দেখাতে হলে:

```sql
SELECT * FROM products;
```

#### 2. 🔍 নির্দিষ্ট কলাম দেখাতে হলে (শুধু name ও price):

```sql
SELECT name, price FROM products;
```

#### 3. 🔎 নির্দিষ্ট ক্যাটাগরির প্রোডাক্ট দেখাতে হলে (যেমন: category_id = 1 → Electronics):

```sql
SELECT * FROM products WHERE category_id = 1;
```

#### 4. 🔝 Price অনুসারে সাজাতে হলে (সস্তা থেকে দামি):

```sql
SELECT * FROM products ORDER BY price ASC;
```

#### 5. 💰 শুধু সেই প্রোডাক্ট দেখাতে হলে যার দাম ১০০০ টাকার বেশি:

```sql
SELECT * FROM products WHERE price > 1000;
```

#### 6. 🔄 ক্যাটাগরি সহ প্রোডাক্ট দেখাতে হলে (JOIN দিয়ে):

```sql
SELECT products.name AS product_name, categories.name AS category_name
FROM products
INNER JOIN categories ON products.category_id = categories.id;
```

> এখানে আমরা JOIN ব্যবহার করে products এর সাথে categories মিলিয়ে দেখাচ্ছি কোন প্রোডাক্ট কোন ক্যাটাগরিতে আছে।

---
