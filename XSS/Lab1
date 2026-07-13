Lab 1 : Reflected XSS into HTML context with nothing encoded

Objective

Exploit a reflected Cross-Site Scripting (XSS) vulnerability in the search functionality by executing JavaScript using the alert() function.

What is Reflected XSS?

Reflected Cross-Site Scripting (XSS) occurs when user input is immediately reflected back in the webpage without proper validation or output encoding. If the application treats the input as HTML instead of plain text, an attacker can inject JavaScript that executes in the victim's browser.

Procedure :

Step 1

Open the lab and click Access the Lab.

Step 2

Locate the search bar on the website.

Step 3

Enter the following payload into the search box:

<script>alert(1)</script>
Step 4

Click the Search button.

Step 5

The application reflects the payload directly into the HTML page without encoding it.

Step 6

The browser executes the JavaScript, displaying an alert box.



Payload Used : 

<script>alert(1)</script>

Why It Works

The search input is reflected directly into the HTML response without sanitization or encoding. Because the browser interprets the injected <script> tag as executable code, the JavaScript runs immediately.
