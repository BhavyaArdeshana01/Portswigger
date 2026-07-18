# Lab1: Unprotected Admin Functionality

**Category:** Access Control  
**Difficulty:** Apprentice  

**Lab Link:** https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality

---

## Objective

Discover an exposed administrator panel that lacks proper access control and use it to delete the user **carlos**.

---

## Vulnerability

### Broken Access Control – Unprotected Administrative Functionality

The application exposes an administrator panel without enforcing authentication or authorization. Since the endpoint is publicly accessible, anyone who discovers the URL can perform administrative actions.

---

## Tools Used

- Feroxbuster
- Web Browser

---

## Steps

### Step 1: Enumerate Hidden Directories

Use **Feroxbuster** to enumerate hidden directories on the target.

```bash
feroxbuster -u https://LAB-ID.web-security-academy.net \
-w /usr/share/seclists/Discovery/Web-Content/common.txt
```

Example Output:

```text
200      GET    /administrator-panel
```

The scan reveals an exposed administrator panel.

---

### Step 2: Visit the Administrator Panel

Open the discovered URL in your browser.

```text
https://LAB-ID.web-security-academy.net/administrator-panel
```

Since there are no access control checks, the administrator interface is accessible.

---

### Step 3: Delete the User

Inside the administrator panel:

1. Locate the user **carlos**
2. Click **Delete**
3. The lab is solved.

---

## Root Cause

The application does not verify whether the current user is authorized to access administrative functionality.

The developers relied on the administrator URL being "hidden" instead of implementing proper authorization checks.

Attackers can easily discover hidden endpoints using:

- Directory brute forcing
- robots.txt
- JavaScript files
- Backup files
- Source code disclosure

---

## Impact

An attacker can:

- Access administrator functionality
- Delete user accounts
- Modify sensitive information
- Perform privileged actions without authentication

---

## Prevention

- Protect every administrative endpoint with server-side authorization.
- Implement Role-Based Access Control (RBAC).
- Return **403 Forbidden** for unauthorized users.
- Never rely on hidden URLs as a security measure.
- Regularly audit exposed administrative endpoints.

---

## Key Takeaways

- Hidden URLs are **not** security.
- Administrative pages must always verify user permissions.
- Directory enumeration tools like **Feroxbuster** can quickly discover exposed endpoints.
- Broken Access Control is one of the most common and critical web application vulnerabilities.

---

## Commands Used

```bash
# Directory Enumeration
feroxbuster -u https://LAB-ID.web-security-academy.net \
-w /usr/share/seclists/Discovery/Web-Content/common.txt

# Open the discovered admin panel
https://LAB-ID.web-security-academy.net/administrator-panel

# Delete the user "carlos"
```

---

## Lab Summary

| Field | Value |
|--------|-------|
| Vulnerability | Broken Access Control |
| Technique | Directory Enumeration |
| Tool | Feroxbuster |
| Exploitation | Access exposed admin panel |
| Impact | Unauthorized administrative access |
| Result | Deleted user **carlos** and solved the lab |

---

**Author:** Bhavya Ardeshana  
**Platform:** PortSwigger Web Security Academy
