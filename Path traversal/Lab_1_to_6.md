# Path Traversal Labs

**Category:** Path Traversal (Directory Traversal)  
**Difficulty:** Apprentice → Practitioner → Expert

**Labs:** https://portswigger.net/web-security/all-labs#path-traversal

---

## Objective

Exploit a Path Traversal vulnerability to access files outside the intended web directory.

Most labs require retrieving the contents of sensitive files such as:

```text
/etc/passwd
```

---

## Vulnerability

### Path Traversal (Directory Traversal)

A Path Traversal vulnerability occurs when an application does not properly validate user-controlled file paths.

An attacker can use sequences such as:

```text
../../../
```

to escape the intended directory and access sensitive files on the server.

---

## Tools Used

- Burp Suite Professional
- Burp Intruder
- Web Browser
- Custom Path Traversal Payload List

---

## Steps

### Step 1: Open the Lab

Launch the PortSwigger Path Traversal lab.

---

### Step 2: Intercept the Request

1. Open **Burp Suite**.
2. Go to **Proxy**.
3. Turn **Intercept ON**.
4. Refresh the lab page.
5. Click **Forward** until you capture the request that loads an image.

Example:

```http
GET /image?filename=218.jpg HTTP/2
```

---

### Step 3: Send to Intruder

Right-click the request.

Select:

```
Send to Intruder
```

---

### Step 4: Configure Payload Position

Highlight only the image filename.

Example:

```http
filename=§218.jpg§
```

Clear all other payload positions.

---

### Step 5: Add Payloads

Paste your Path Traversal payload list into **Payload Set 1**.

Example payloads:

```text
../../../etc/passwd
../../../../etc/passwd
../../../../../etc/passwd
..%2f..%2f..%2fetc/passwd
```

> I used my own Path Traversal payload list to automate testing. :contentReference[oaicite:1]{index=1}

---

### Step 6: Start the Attack

Click:

```
Start Attack
```

Burp Intruder automatically tests every payload against the vulnerable parameter.

---

### Step 7: Analyze the Results

Look for a response that:

- Returns **HTTP 200**
- Has a larger response size
- Contains the contents of:

```text
root:x:0:0:
daemon:x:1:1:
```

This indicates that the payload successfully accessed:

```text
/\
etc/passwd
```

Once the correct payload is identified, the lab is solved.

---

## Root Cause

The application does not properly validate file paths supplied by the user.

Instead of restricting access to the intended directory, it allows directory traversal sequences such as:

```text
../
```

allowing attackers to read arbitrary files from the server.

---

## Impact

An attacker may be able to:

- Read sensitive system files
- Access application source code
- Retrieve configuration files
- Obtain credentials
- Gather information for further attacks

---

## Prevention

- Validate all user-supplied file paths.
- Use allowlists for permitted files.
- Normalize file paths before use.
- Restrict file access to specific directories.
- Never directly concatenate user input into filesystem paths.

---

## Key Takeaways

- Path Traversal allows attackers to escape the intended directory.
- Burp Intruder makes testing multiple payloads much faster.
- Different encoding techniques can bypass input validation.
- Always validate and sanitize file path input on the server.

---

## Workflow

```text
1. Open the lab.
2. Enable Intercept in Burp Suite.
3. Refresh the page.
4. Capture the image request.
5. Send the request to Intruder.
6. Mark the filename parameter as the payload position.
7. Paste the Path Traversal payload list.
8. Start the attack.
9. Identify the payload that retrieves /etc/passwd.
10. The lab is solved.
```

---

## Lab Summary

| Field | Value |
|--------|-------|
| Vulnerability | Path Traversal |
| Category | File Path Manipulation |
| Tool | Burp Suite Professional |
| Module | Intruder |
| Attack Type | Sniper |
| Payload | Custom Path Traversal Payload List |
| Target File | /etc/passwd |
| Result | Successfully accessed sensitive server files |

---

**Author:** Bhavya Ardeshana  
**Platform:** PortSwigger Web Security Academy
