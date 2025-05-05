
## 🛠️ **DML (Data Manipulation Language)**

**DML (Data Manipulation Language)** ব্যবহার করা হয় ডেটাবেসের **ডেটা ইনসার্ট**, **আপডেট**, **মুছে ফেলা**, বা **ব্যবহারকারীভিত্তিক পরিবর্তন** করার জন্য।

###  প্রধান DML কমান্ড:

1. `INSERT` – ডেটা যোগ করা
    
2. `UPDATE` – ডেটা আপডেট/পরিবর্তন করা
    
3. `DELETE` – ডেটা মুছে ফেলা
    
---

### 🛒 ধরি, আমাদের তিনটি টেবিল আছে:

#### 1. `categories`

```sql
CREATE TABLE categories (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100)
);
```

#### 2. `products`

```sql
CREATE TABLE products (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  price DECIMAL(10,2),
  category_id INT,
  FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

#### 3. `customers`

```sql
CREATE TABLE customers (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  email VARCHAR(100)
);
```

---

## ✅ **INSERT** (তথ্য যোগ করা):

#### 🔹 ক্যাটাগরি টেবিলে ডেটা ইনসার্ট:

```sql
INSERT INTO categories (name) VALUES ('Electronics'), ('Fashion');
```

#### 🔹 প্রোডাক্ট টেবিলে ডেটা ইনসার্ট:

```sql
INSERT INTO products (name, price, category_id)
VALUES ('Smartphone', 15000.00, 1),
       ('Jeans', 1200.00, 2);
```

#### 🔹 কাস্টমার টেবিলে ডেটা ইনসার্ট:

```sql
INSERT INTO customers (name, email)
VALUES ('Rahim Uddin', 'rahim@example.com');
```

---

## 🛠️ **UPDATE** (তথ্য পরিবর্তন করা):

#### 🔄 প্রোডাক্টের দামের পরিবর্তন:

```sql
UPDATE products
SET price = 14000.00
WHERE name = 'Smartphone';
```

#### 🧑 কাস্টমারের নাম আপডেট:

```sql
UPDATE customers
SET name = 'Rahim Chowdhury'
WHERE id = 1;
```

---

## ❌ **DELETE** (তথ্য মুছে ফেলা):

#### ❌ নির্দিষ্ট প্রোডাক্ট মুছে ফেলা:

```sql
DELETE FROM products
WHERE name = 'Jeans';
```

#### ❌ নির্দিষ্ট ক্যাটাগরি মুছে ফেলা (যদি ফোরেইন কি কনস্ট্রেইন্ট না থাকে):

```sql
DELETE FROM categories
WHERE name = 'Fashion';
```

---

## 📌 সংক্ষেপে DML:

|Command|কাজ|উদাহরণ|
|---|---|---|
|`INSERT`|নতুন রেকর্ড যোগ করা|`INSERT INTO products (...) VALUES (...);`|
|`UPDATE`|বিদ্যমান রেকর্ড আপডেট|`UPDATE products SET price = ... WHERE ...;`|
|`DELETE`|রেকর্ড মুছে ফেলা|`DELETE FROM products WHERE id = ...;`|

---

📌 **টিপস**:

- `UPDATE` বা `DELETE` এর আগে `WHERE` ব্যবহার না করলে **সব রেকর্ড** পরিবর্তন/মুছে যেতে পারে — তাই সাবধান!
    
- DML কাজের পর ডেটা **স্থায়ীভাবে সেভ** করার জন্য `COMMIT` ব্যবহার করা হয় (যদি ট্রানজেকশন চালু থাকে)।
    

---
