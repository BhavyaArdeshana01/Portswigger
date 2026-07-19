# Lab3: Password Reset Broken Logic

**Category:** Authentication  
**Difficulty:** Apprentice  

**Lab Link:** https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic

---

## Objective

Exploit a flaw in the password reset functionality to identify valid username and password combinations, then log in to the target account.

---

## Vulnerability

### Broken Authentication – Password Reset Logic

The application contains a flaw in its password reset/login process that can be exploited by automating authentication attempts. By using Burp Suite Intruder with the provided username and password lists, it is possible to discover valid credentials.

---

## Tools Used

- Burp Suite Professional
- Burp Intruder
- Web Browser

---

## Steps

### Step 1: Attempt Login

Visit the login page and enter any random username and password.

Example:

```text
Username: test
Password: test123
```

Click **Log in**.

---

### Step 2: Capture the Request

1. Turn **Intercept ON** in Burp Suite.
2. Submit the login request.
3. Burp captures the HTTP request.

Example:

```http
POST /login HTTP/2

username=test
password=test123
```

---

### Step 3: Send the Request to Intruder

Right-click the intercepted request and select:

```
Send to Intruder
```

---

### Step 4: Configure Payload Positions

Clear any automatically selected payload positions.

Highlight the following parameters:

```text
username=
password=
```

Click **Add** so that both parameters become payload positions.

---

### Step 5: Add Username and Password Lists

The lab provides:

- Username list
- Password list

Copy the usernames into **Payload Set 1**.

Copy the passwords into **Payload Set 2**.

Configure the attack type as:

```
Cluster Bomb
```

This tests every username against every password.

---

### Step 6: Start the Attack

Click:

```
Start Attack
```

Burp Intruder will try every possible username/password combination.

Example:

| Username | Password | Status |
|----------|----------|--------|
| alice | password | 200 |
| bob | qwerty | 302 |
| carlos | abc123 | 200 |

Look for responses with:

- Different response length
- Different status code
- Redirect (302)
- Successful login indicator

These usually indicate valid credentials.

---

### Step 7: Login with Valid Credentials

After identifying the correct username and password, return to the login page.

Enter the valid credentials and log in.

The lab is now solved.

---

## Root Cause

The application allows unlimited authentication attempts without proper protections such as:

- Account lockout
- Rate limiting
- CAPTCHA
- Multi-factor authentication

This enables attackers to automate credential testing using tools like Burp Intruder.

---

## Impact

An attacker could:

- Discover valid usernames
- Perform brute-force attacks
- Gain unauthorized access
- Compromise user accounts

---

## Prevention

- Implement rate limiting.
- Lock accounts after multiple failed login attempts.
- Require Multi-Factor Authentication (MFA).
- Use CAPTCHA after repeated failures.
- Monitor and alert on excessive login attempts.

---

## Key Takeaways

- Burp Intruder is effective for automating authentication testing.
- Cluster Bomb attacks test every username against every password.
- Weak authentication controls make brute-force attacks practical.
- Proper account protection mechanisms significantly reduce this risk.

---

## Commands / Workflow

```text
1. Attempt login with random credentials.
2. Intercept the request using Burp Suite.
3. Send the request to Intruder.
4. Mark the username and password fields as payload positions.
5. Paste the provided username list into Payload Set 1.
6. Paste the provided password list into Payload Set 2.
7. Select Cluster Bomb attack type.
8. Start the attack.
9. Identify the successful response.
10. Log in using the discovered credentials.
```

---

## Lab Summary

| Field | Value |
|--------|-------|
| Vulnerability | Broken Authentication |
| Technique | Brute Force |
| Tool | Burp Suite Professional |
| Module | Intruder |
| Attack Type | Cluster Bomb |
| Result | Discovered valid credentials and logged in |

---

**Author:** Bhavya Ardeshana  
**Platform:** PortSwigger Web Security Academy
