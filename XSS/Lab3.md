# Lab 3: DOM XSS in `document.write` Sink Using Source `location.search`

## 🎯 Objective

Exploit a DOM-Based Cross-Site Scripting (DOM XSS) vulnerability by injecting JavaScript through the search functionality, causing the browser to execute the `alert()` function.

---

## 📖 What is DOM-Based XSS?

DOM-Based Cross-Site Scripting (DOM XSS) occurs when client-side JavaScript reads data from a user-controllable source, such as the URL or search parameter, and writes it to the webpage using an unsafe DOM sink like `document.write()`, `innerHTML`, or `eval()`. Unlike Reflected or Stored XSS, the vulnerability exists entirely in the browser's JavaScript rather than the server-side application. :contentReference[oaicite:0]{index=0}

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Use the **Search** functionality and enter any random text.

Example:

```text
test
```

### Step 3

Inspect the page using your browser's **Developer Tools** and observe that the search term is inserted into an `<img>` element using the JavaScript `document.write()` function.

### Step 4

Replace the search value with the following payload:

```html
"><svg onload=alert(1)>
```

### Step 5

Press **Search**.

### Step 6

The payload breaks out of the existing HTML attribute and injects a new `<svg>` element with an `onload` event.

### Step 7

The browser executes the JavaScript and displays an alert box.

### Step 8

The lab is marked as **Solved**.

---

## 💻 Payload Used

```html
"><svg onload=alert(1)>
```

---

## ⚙️ Why It Works

The application reads user input from the `location.search` parameter and inserts it into the page using the `document.write()` sink without proper sanitization or encoding. By breaking out of the existing HTML attribute and injecting an SVG element with an `onload` event, arbitrary JavaScript is executed in the browser. :contentReference[oaicite:1]{index=1}

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

- Never insert untrusted data into `document.write()`.
- Use safe DOM APIs such as `textContent` instead of writing raw HTML.
- Validate and sanitize user-controlled input.
- Encode output according to the HTML context.
- Implement a strong Content Security Policy (CSP).

---

## 🛠️ Tools Used

- Web Browser
- Browser Developer Tools (Inspect Element)
- PortSwigger Web Security Academy

---

## 📸 Screenshots

Add screenshots for:

1. Lab overview page
2. Search functionality
3. Inspect Element showing `document.write()`
4. Payload entered
5. Alert popup
6. Lab solved confirmation

---

## 🏁 Conclusion

This lab demonstrates how insecure client-side JavaScript can introduce a DOM-Based XSS vulnerability. Since the application writes attacker-controlled data from `location.search` directly into the DOM using `document.write()`, an attacker can inject HTML and JavaScript that executes in the victim's browser. Avoiding unsafe DOM sinks and properly handling untrusted input are essential to preventing DOM XSS. 
