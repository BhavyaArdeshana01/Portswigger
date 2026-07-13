# Lab 1: Reflected XSS into HTML Context with Nothing Encoded

## 🎯 Objective

Exploit a Reflected Cross-Site Scripting (XSS) vulnerability in the search functionality by executing JavaScript using the `alert()` function.

---

## 📖 What is Reflected XSS?

Reflected Cross-Site Scripting (XSS) occurs when user input is immediately reflected back in the webpage without proper validation or output encoding. If the application treats the input as HTML instead of plain text, an attacker can inject JavaScript that executes in the victim's browser.

---

## 🚀 Procedure

### Step 1
Open the lab and click **Access the Lab**.

### Step 2
Locate the **Search** bar on the website.

### Step 3
Enter the following payload into the search box:

```html
<script>alert(1)</script>
```

### Step 4
Click the **Search** button.

### Step 5
The application reflects the payload directly into the HTML page without encoding it.

### Step 6
The browser executes the JavaScript, displaying an alert box.

### Step 7
The lab is marked as **Solved**.

---

## 💻 Payload Used

```html
<script>alert(1)</script>
```

---

## ⚙️ Why It Works

The search input is reflected directly into the HTML response without sanitization or output encoding. Because the browser interprets the injected `<script>` tag as executable code, the JavaScript executes immediately.

---

## 🛡️ Remediation

- Validate all user input.
- Encode output before rendering it in HTML.
- Sanitize user-controlled data.
- Implement a strong Content Security Policy (CSP).

---

## 📸 Screenshots

> Add screenshots of the following:
>
> - Lab overview page
> - Search bar
> - Payload entered
> - `alert(1)` popup
> - Lab solved confirmation

---

## 🏁 Conclusion

This lab demonstrates how failing to encode user input can lead to a Reflected XSS vulnerability. Proper input validation and output encoding are essential to prevent attackers from executing arbitrary JavaScript in users' browsers.
