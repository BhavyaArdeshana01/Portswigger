# Lab 7: Reflected XSS into Attribute with Angle Brackets HTML-Encoded

## 🎯 Objective

Exploit a Reflected Cross-Site Scripting (XSS) vulnerability where angle brackets (`<` and `>`) are HTML-encoded, but user input is reflected inside an HTML attribute. Execute JavaScript using the `onmouseover` event.

---

## 📖 What is Reflected XSS?

Reflected Cross-Site Scripting (XSS) occurs when user input is immediately reflected in the application's response without proper validation or output encoding. In this lab, the application encodes angle brackets, preventing direct `<script>` injection. However, because the input is reflected inside an HTML attribute, it is still possible to inject an event handler that executes JavaScript.

---

## 🚀 Procedure

### Step 1

Open the lab and click **Access the Lab**.

### Step 2

Locate the **Search** bar on the website.

### Step 3

Enter the following payload into the search box:

```html
" onmouseover="alert()"
```

### Step 4

Click the **Search** button.

### Step 5

The application reflects the payload inside the `value` attribute of the search input field.

### Step 6

Inspect the page using the browser's Developer Tools.

You will notice that the input field becomes similar to:

```html
<input
type="text"
value="YOUR_INPUT"
onmouseover="alert()"
>
```

### Step 7

Move your mouse pointer over the search input field.

### Step 8

The `onmouseover` event is triggered, executing the JavaScript and displaying an alert box.

### Step 9

The lab is marked as **Solved**.

---

## 💻 Payload Used

```html
" onmouseover="alert()"
```

---

## ⚙️ Why It Works

Although the application encodes the `<` and `>` characters, it fails to escape quotation marks inside the HTML attribute. By injecting a double quote (`"`), the original `value` attribute is terminated, allowing a new attribute (`onmouseover`) to be added. When the user moves the mouse over the input field, the injected JavaScript executes.

---

## 🛠️ Tools Used

- Google Chrome
- Chrome Developer Tools
- PortSwigger Web Security Academy

## 🏁 Conclusion

This lab demonstrates that HTML encoding of angle brackets alone is insufficient to prevent XSS attacks. If quotation marks inside HTML attributes are not properly escaped, an attacker can inject new attributes containing JavaScript event handlers such as `onmouseover`, leading to successful code execution.
