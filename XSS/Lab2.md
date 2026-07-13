# Lab 2: Stored XSS into HTML Context with Nothing Encoded

## 🎯 Objective

Exploit a Stored Cross-Site Scripting (XSS) vulnerability in the blog comment functionality by injecting JavaScript that executes when the page is viewed.

---

## 📖 What is Stored XSS?

Stored Cross-Site Scripting (Stored XSS), also known as **Persistent XSS**, occurs when malicious user input is stored by the application (such as in a database) and later displayed to users without proper validation or output encoding. As a result, the injected JavaScript executes whenever anyone views the affected page. :contentReference[oaicite:0]{index=0}

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Open any blog post.

### Step 3

Scroll down to the **Leave a comment** section.

### Step 4

Fill in the required fields:

- **Comment:** `<script>alert(1)</script>`
- **Name:** Your name
- **Email:** Any valid email address
- **Website:** Any URL (optional if accepted)

### Step 5

Click **Post Comment**.

### Step 6

The application stores the submitted comment and displays it on the blog page without encoding the HTML.

### Step 7

When the page reloads, the browser executes the injected JavaScript and displays an alert box.

### Step 8

The lab is marked as **Solved**.

---

## 💻 Payload Used

```html
<script>alert(1)</script>
```

---

## ⚙️ Why It Works

The application stores user input and later renders it directly into the HTML page without sanitizing or encoding it. Because the browser interprets the `<script>` tag as executable JavaScript, the payload runs whenever the blog post is viewed. :contentReference[oaicite:1]{index=1}

---

## 🏁 Conclusion

This lab demonstrates how storing unsanitized user input can lead to a **Stored XSS** vulnerability. Unlike Reflected XSS, the malicious payload is saved by the application and executes automatically whenever the affected page is viewed, making it more dangerous because it can impact multiple users. :contentReference[oaicite:2]{index=2}
