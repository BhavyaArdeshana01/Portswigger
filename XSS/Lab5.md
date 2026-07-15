# Lab 5: DOM XSS in jQuery Anchor `href` Attribute Sink Using `location.search` Source

## 🎯 Objective

Exploit a DOM-Based Cross-Site Scripting (DOM XSS) vulnerability by manipulating the `returnPath` parameter so that clicking the **Back** link executes JavaScript and displays the user's cookies using `alert(document.cookie)`.

---

## 📖 What is DOM-Based XSS?

DOM-Based Cross-Site Scripting (DOM XSS) occurs when client-side JavaScript reads data from a user-controlled source, such as the URL, and writes it into the Document Object Model (DOM) using an unsafe sink. In this lab, the application reads the `returnPath` parameter from the URL and assigns it directly to the `href` attribute of the **Back** link without validation. :contentReference[oaicite:0]{index=0}

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Navigate to the **Submit Feedback** page.

### Step 3

Observe that the URL contains the following parameter:

```text
?returnPath=/
```

### Step 4

Replace the `returnPath` value with the following payload:

```text
javascript:alert(document.cookie)
```

Example:

```text
https://YOUR-LAB-ID.web-security-academy.net/feedback?returnPath=javascript:alert(document.cookie)
```

### Step 5

Press **Enter** to load the modified URL.

### Step 6

Click the **Back** link displayed on the page.

### Step 7

The browser executes the JavaScript payload and displays the cookies using `alert(document.cookie)`.

### Step 8

The lab is marked as **Solved**.

---

## 💻 Payload Used

```text
javascript:alert(document.cookie)
```

---

## ⚙️ Why It Works

The application reads the value of the `returnPath` parameter from the URL and assigns it directly to the `href` attribute of the **Back** link using jQuery. Since no validation is performed, the `javascript:` URI scheme is accepted. When the user clicks the link, the browser executes the JavaScript contained in the `href` attribute instead of navigating to another page. :contentReference[oaicite:1]{index=1}

---

## 💥 Impact

A successful DOM XSS attack can allow an attacker to:

- Execute arbitrary JavaScript
- Steal session cookies (if they are not protected with the `HttpOnly` flag)
- Hijack user sessions
- Redirect users to malicious websites
- Modify webpage content
- Perform actions on behalf of authenticated users

---

## 🛡️ Remediation

- Never assign untrusted user input directly to the `href` attribute.
- Validate and sanitize all URL parameters.
- Reject dangerous URI schemes such as `javascript:`.
- Use allowlists for valid URLs.
- Implement a strong Content Security Policy (CSP).

---

## 🏁 Conclusion

This lab demonstrates a DOM-Based XSS vulnerability caused by assigning user-controlled input directly to an anchor element's `href` attribute. By injecting a `javascript:` URI into the `returnPath` parameter, an attacker can execute arbitrary JavaScript when the user clicks the **Back** link. Proper URL validation and safe handling of user input are essential to prevent this type of vulnerability. :contentReference[oaicite:2]{index=2}
