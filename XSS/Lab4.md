# Lab 4: DOM XSS in `innerHTML` Sink Using Source `location.search`

## 🎯 Objective

Exploit a DOM-Based Cross-Site Scripting (DOM XSS) vulnerability by injecting a malicious HTML payload into the search functionality, causing JavaScript to execute in the browser.

---

## 📖 What is DOM-Based XSS?

DOM-Based Cross-Site Scripting (DOM XSS) occurs when client-side JavaScript reads data from a user-controlled source, such as the URL or search parameter, and inserts it into the webpage using an unsafe DOM sink like `innerHTML`. Since the vulnerability exists in the browser's JavaScript rather than the server, the malicious payload executes entirely on the client side. :contentReference[oaicite:0]{index=0}

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Locate the **Search** bar on the website.

### Step 3

Enter the following payload into the search box:

```html
<img src=1 onerror=alert(1)>
```

### Step 4

Click the **Search** button.

### Step 5

The application inserts the search value into the page using the `innerHTML` property without proper sanitization.

### Step 6

The browser attempts to load the invalid image (`src=1`), triggering the `onerror` event.

### Step 7

The JavaScript `alert(1)` executes, displaying an alert box.

### Step 8

The lab is marked as **Solved**.

---

## 💻 Payload Used

```html
<img src=1 onerror=alert(1)>
```

---

## ⚙️ Why It Works

The application takes input from the `location.search` parameter and inserts it into the page using the `innerHTML` sink. Although modern browsers do not execute `<script>` tags inserted via `innerHTML`, event handlers such as `onerror` still execute. Because the image source is invalid, the `onerror` event fires and the JavaScript payload runs successfully. :contentReference[oaicite:1]{index=1}

---

## 💥 Impact

A successful DOM XSS attack can allow an attacker to:

- Execute arbitrary JavaScript
- Steal session cookies
- Hijack user sessions
- Redirect users to malicious websites
- Modify webpage content
- Perform actions on behalf of authenticated users

---

## 🛡️ Remediation

- Avoid using `innerHTML` with untrusted user input.
- Use `textContent` or `innerText` when displaying user-controlled data.
- Validate and sanitize all user input.
- Implement a strong Content Security Policy (CSP).
- Use secure DOM manipulation methods that automatically escape HTML.

---

## 🏁 Conclusion

This lab demonstrates how using `innerHTML` with untrusted user input can lead to a DOM-Based XSS vulnerability. Even though `<script>` tags inserted through `innerHTML` are not executed by modern browsers, attackers can still execute JavaScript using HTML event handlers such as `onerror`. Developers should avoid unsafe DOM sinks and safely handle all user-controlled input. :contentReference[oaicite:2]{index=2}
