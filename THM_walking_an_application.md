# TryHackMe Web Security Vulnerabilities Walkthrough  
**Room:** Walking an Application  
**Site:** TryHackMe.com  
**Type:** Walkthrough  
**Author:** Jerome Goldwin M.  
**Date:** 2025/04/02  

## 🕵️‍♂️ Exploring the Target  
The vulnerable URL is **`https://lab_web_url.p.thmlabs.com/`**.  
I started exploring the website, diving into different directories and forms.  

### 🔍 Hidden Credentials?  
Found **`/customer/login/`** and checked the source code. Maybe some developer left test credentials?  
❌ Nope, that didn’t work. Moving on...  

### 🎯 First Flag - Hidden in Plain Sight  
Searching the site’s code led me to a hidden secret link.  
✅ **Flag:** `THM{NOT_A_SECRET_ANYMORE}`  

---

## 🚨 Common Security Flaws  

### 1️⃣ **HTML Comments Contain Sensitive Info**  
The framework used is old. I almost missed the first comment pages—  
✅ **Flag:** `THM{HTML_COMMENTS_ARE_DANGEROUS}`  

### 2️⃣ **Directory Listing is Enabled**  
A restricted page wasn’t throwing a `403 Forbidden` error. Instead, it showed all files.  
✅ **Flag:** `THM{INVALID_DIRECTORY_PERMISSION}`  

### 3️⃣ **Default Framework Credentials Exist**  
Visiting `/thm-framework-login`, I used the default credentials:  

username: admin
password: admin

✅ **Flag:** `THM{CHANGE_DEFAULT_CREDENTIALS}`  

---

## 🛠️ Bypassing Security Measures  

### **Changing Log Files Can Reveal Info**  
A `tmp.zip` file wasn’t meant to be public, but the outdated version made it accessible.  
✅ **Flag:** `THM{KEEP_YOUR_SOFTWARE_UPDATED}`  

### **Frontend Security is Not Real Security**  
The "Premium Customers Only" page blocked me… or so it thought.  
I inspected the **HTML elements**, removed the `div.premium-customer-blocker`, and—voilà!  
✅ **Flag:** `THM{NOT_SO_HIDDEN}`  

---

## 🔎 Using Developer Tools  

### 1️⃣ **Catching Hidden JavaScript Flags**  
A red blink appeared on the contact page. Suspicious.  
I opened the **Firefox Debugger**, found `flash.min.js`, pretty-printed it, and boom:  
✅ **Flag:** `THM{CATCH_ME_IF_YOU_CAN}`  

### 2️⃣ **Intercepting Network Requests**  
Using browser **Network Tools**, I filled out the contact form. The **POST request** contained:  
✅ **Flag:** `THM{GOT_AJAX_FLAG}`  

---

## 🎯 Conclusion  
This was a fun and insightful security walkthrough! **Key takeaways:**  
✅ **Always check for exposed credentials, outdated software, and improper permissions.**  
✅ **Client-side security is not real security—inspect, modify, and bypass.**  
✅ **Dev tools are powerful! Understand how they work.**
