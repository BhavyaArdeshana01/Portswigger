# Lab 1: Username Enumeration via Different Responses

**Category:** Authentication  
**Difficulty:** Apprentice  

**Lab Link:** https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses

---

## Objective

Identify a valid username by observing differences in the application's login responses. Once a valid username is found, brute-force its password using the provided password list and log in to solve the lab. :contentReference[oaicite:0]{index=0}

---

## Vulnerability

### Username Enumeration via Different Responses

The application returns different error messages depending on whether the username exists.

- **Invalid username** → Username does not exist.
- **Incorrect password** → Username exists, but the password is incorrect.

These different responses allow an attacker to enumerate valid usernames before attempting a password brute-force attack. :contentReference[oaicite:1]{index=1}

---

## Tools Used

- Burp Suite Professional
- Burp Intruder
- Web Browser

---

## Steps

### Step 1: Intercept the Login Request

1. Open the lab.
2. Turn **Intercept ON** in Burp Suite.
3. Enter any random credentials.

Example:

```text
Username: test
Password: test123
```

4. Click **Log in**.

Burp captures the login request.

---

### Step 2: Send the Request to Intruder

Right-click the intercepted request and select:

```
Send to Intruder
```
### Step 3: Configure Burp Intruder

1. Clear all automatically selected payload positions.
2. Select both the **username** and **password** parameters.
3. Click **Add** so both become payload positions.

Example:

```http
POST /login HTTP/2

username=§test§
password=§test123§
```

Select the attack type:

```
Attack Type → Cluster Bomb
```

---

### Step 4: Add Payloads

The lab provides:

- Username list
- Password list

Configure the payloads as follows:

- **Payload Set 1:** Username list
- **Payload Set 2:** Password list

Click **Start Attack**.

Burp Intruder will test every username with every password combination.

---

### Step 5: Analyze the Results

Review the Intruder results.

Look for a response with:

- **HTTP Status:** `302 Found`
- A different response length
- A redirect to another page

The request with these characteristics contains the **valid username and password** combination.

---

### Step 6: Login

Use the discovered username and password to log in.

The lab is now solved.

### Step 7: Find the Correct Password

Review the Intruder results.

Most responses return:

```text
Status: 200
```

One request returns:

```text
Status: 302
```

The **302 Redirect** indicates a successful login.

Make a note of the corresponding password. :contentReference[oaicite:3]{index=3}

---

### Step 8: Login

Return to the login page.

Enter:

- Valid Username
- Valid Password

Click **Log in**.

The lab is now solved.

---

## Root Cause

The application leaks information by returning different authentication error messages.

Instead of using a generic response for all failed login attempts, it distinguishes between:

- Invalid usernames
- Incorrect passwords

This enables attackers to enumerate valid accounts before launching password attacks. :contentReference[oaicite:4]{index=4}

---

## Impact

An attacker can:

- Discover valid usernames
- Reduce brute-force attempts
- Increase the success rate of password attacks
- Gain unauthorized access to user accounts

---

## Prevention

- Return the same error message for all failed login attempts.
- Ensure response lengths and status codes are identical.
- Implement rate limiting.
- Enable account lockout after repeated failures.
- Require Multi-Factor Authentication (MFA).
- Log and monitor repeated authentication failures.

---

## Key Takeaways

- Different authentication responses can leak sensitive information.
- Username enumeration is often the first step in a brute-force attack.
- Burp Intruder makes automated username testing easy.
- Generic error messages help prevent information disclosure.

---

## Workflow

```text
1. Intercept the login request.
2. Send the request to Burp Intruder.
3. Select only the username as the payload position.
4. Use Sniper attack.
5. Paste the provided username list.
6. Identify the valid username from the different response.
7. Replace the username with the valid one.
8. Select only the password as the payload position.
9. Paste the provided password list.
10. Start the attack.
11. Identify the successful login (HTTP 302).
12. Log in using the discovered credentials.
```

---

## Lab Summary

| Field | Value |
|--------|-------|
| Vulnerability | Username Enumeration |
| Category | Authentication |
| Tool | Burp Suite Professional |
| Module | Intruder |
| Attack Type | Cluster Bomb |
| Enumeration Method | Different Error Messages |
| Password Attack | Brute Force |
| Result | Logged in with valid credentials |

---

**Author:** Bhavya Ardeshana  
**Platform:** PortSwigger Web Security Academy
