# AppSec_DAST_OWASP_ZAP
# OWASP Juice Shop Security Assessment with OWASP ZAP- a DAST tool

## Overview
This project demonstrates a **Comprehensive Web Application Security Assessment** of the intentionally vulnerable **OWASP Juice Shop** using **OWASP ZAP** for Dynamic Application Security Testing (DAST).

### Objectives
- Explore web crawling techniques: **traditional spidering** and **AJAX crawling**
- Perform **passive scanning** as well as **active vulnerability scanning**
- Identify key vulnerabilities including:
  - **SQL Injection**
  - **Cross-Site Scripting** (Reflected, Stored, DOM)
  - **Authentication bypass**
  - **Broken access control**
- Leverage **automated testing workflows**
- Generate downloadable scan reports and link to them

## Tools & Setup

1. **OWASP Juice Shop**
   - A modern, JavaScript-heavy insecure web application built with Node.js, Express, and Angular. It intentionally includes vulnerabilities from the OWASP Top 10
     Form Sources- 
          1.	Install node.js
          2.	Run git clone https://github.com/juice-shop/juice-shop.git --depth 1 (or clone your own fork of the repository)
          3.	Go into the cloned folder with cd juice-shop
          4.	Run npm install (only has to be done before first start or when you change the source code)
          5.	Run npm start
          6.	Browse to http://localhost:3000

    Docker Container- 
          1.	Install Docker
          2.	docker pull bkimminich/juice-shop
          3.	docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop
          4.	Browse to http://localhost:3000 (on macOS and Windows browse to http://192.168.99.100:3000 if you are using docker-machine instead of the native docker installation)
   
3. **OWASP ZAP (Zed Attack Proxy)**
   - An open-source, flagship OWASP DAST tool with intercepting proxy, traditional + AJAX spiders, passive and active scanning, scripting, and reporting capabilities
     
4. **Environment**
   - Run Juice Shop locally (via Docker or Node.js) and point ZAP at the target URL (e.g., `http://localhost:3000`) 

## Testing Methodology

### 1. Spidering
- **Traditional Spider**: Crawls through hyperlinks to map site structure.
  
Navigate to:  ```Tools--> Spider```

  ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/2.1%20Spider.png)

- **AJAX Spider**: Handles JavaScript-heavy or single-page applications by discovering dynamically loaded content via AJAX calls.
  
Navigate to: ```Tools--> AJAX Spider```

![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/2.%20AJAX%20Spider.png)

### 2. Scanning
- **Passive Scanning**  
  - Listens and analyzes HTTP traffic without sending malicious payloads.
  - Identifies issues like missing headers, information leakage, etc.
  
  Navigate to: ```Manual Explore```
![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/4.1%20Passive%20Scan%20Rules.png)
  
- **Active Scanning**  
  - Sends crafted malicious requests to identify deeper vulnerabilities.
  - Should be run **only** in a safe, test environment (like a local Juice Shop instance).
    
    Navigate to: ```Automate Explore```
    
    ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/4.1%20Passive%20Scan%20Rules.png)

## 3. Vulnerabilities Tested

### 3a. SQL Injection (SQLi)
- Attempt to inject SQL statements into input fields.
- Review ZAP findings for database error messages or abnormal behaviors.

### 3b. Cross-Site Scripting (XSS)
- **Reflected XSS**: Payloads sent in URLs and reflected in HTTP responses.
- **Stored XSS**: Payload stored on the server and displayed to other users.
- **DOM-based XSS**: Payload executed entirely within the browser via JavaScript DOM manipulation.

### 3c. Authentication Bypass
- Test login and session management for weaknesses allowing unauthorized access.

### 3d. Broken Access Control
**Definition:**  
Broken Access Control occurs when applications fail to enforce permissions properly, allowing unauthorized users to access restricted data or functions.

**Steps Taken:**  
1. Created a regular user account in Juice Shop.  
2. Configured OWASP ZAP as an intercepting proxy to capture HTTP requests.  
3. Intercepted the registration request containing a JSON body with `"role": "customer"`.  
4. Modified the `"role"` parameter to `"admin"` before forwarding the request.  

**Result:**  
- The server accepted the modified request without validation.  
- The new user account was created with **administrator privileges**, granting access to all admin functionalities.  

**Key Takeaway:**  
Servers must **never trust client-supplied role or permission data**. Always enforce role-based access control at the server side.

---
### 3f. Directory Traversal
**Definition:**  
A Directory Traversal vulnerability allows attackers to read files outside the intended directory by manipulating request file paths using patterns like `../`.

Plain Explanation:
This is when a hacker tricks a website into giving them files they’re not supposed to see by sneaking into hidden folders.
It’s like finding a secret hallway in a hotel that leads you to the manager’s office instead of your guest room.

Example in Real Life:
You rent a storage locker, but instead of opening only your own, you figure out a way to open other people’s lockers too.

Example in Web Apps:
A site lets you download your invoice:

https://example.com/download?file=my_invoice.pdf


A hacker changes it to:

https://example.com/download?file=../../passwords.txt


The ../../ means “go up two folders” — now the server gives them sensitive files from outside the normal folder.
**Steps Taken:**  
1. Navigated to the **Photo Wall** feature and inspected the **file download requests** in the browser developer tools.  
2. Observed that the file path was passed as a parameter in the request.  
3. Modified the path parameter to include directory traversal sequences (`../`) to move up the file system hierarchy.  
4. Requested sensitive files such as server configuration data.  

**Result:**  
- Successfully retrieved sensitive files stored outside the web root.  
- Confirmed the application did not sanitize file path input properly.

**Key Takeaway:**  
Applications must sanitize and validate file paths and **disallow traversal sequences** to prevent unauthorized file disclosure.


### 3. Cross-Site Request Forgery (CSRF)

**Definition:**  
CSRF forces an authenticated user to unintentionally execute actions on a web application in which they are logged in.
Plain Explanation:
This happens when a system fails to check whether someone is allowed to do something.
It’s like a security guard letting anyone into the VIP lounge without checking if they have the right badge.

Example in Real Life:
Imagine a cinema where you buy a ticket for a normal seat, but the doors to the premium seats aren’t locked. You simply walk in and sit there — no one stops you.

Example in Web Apps:
A normal user’s account shouldn’t let them see admin pages. But if the website doesn’t check permissions properly, they could just type:

https://example.com/admin


…and get in without being an admin.
Plain Explanation:
This is when a hacker tricks you into doing something on a site you’re logged into — without you realizing it.
It’s like a con artist giving you a form to sign, telling you it’s a petition, but in reality, it’s a cheque from your bank account.

Example in Real Life:
You’re logged into your online banking on one tab. On another tab, you visit a funny meme site. The meme site secretly sends a request to your bank to transfer money — and since you’re already logged in, the bank thinks you made the request.

Example in Web Apps:
If you’re logged into shopping.com and you click on a malicious link:

http://shopping.com/change_email?email=hacker@example.com


…the site updates your email address without asking, because it trusted your browser.

**Steps Taken:**  
1. Logged into Juice Shop with a standard user account.  
2. Identified the `POST /profile` request responsible for updating the display name.  
3. Crafted a **malicious HTML page** containing a form that auto-submitted a request to change the display name.  
4. Hosted the page locally using:
   ```python3 -m http.server 8081```

6. While logged in to Juice Shop, visited the malicious page in another browser tab.  

**Result:**  
- The browser automatically sent the authenticated request, changing the profile name to `HackedByCSRF`.  

**Key Takeaway:**  
CSRF can be prevented by implementing:
- Anti-CSRF tokens
- SameSite cookie attributes
- Double-submit cookie patterns



### 3f. Denial of Service (DoS)
- Identify endpoints susceptible to resource exhaustion.
- 

## 4. Automated Scanning & Report Generation
- Use ZAP’s CLI or API to automate spidering + active scanning in a single script.
- Schedule scans or integrate into CI/CD pipelines.
- Example steps:
1. Forward Selenium browser traffic through ZAP proxy.
2. After Selenium tests complete, call:

## 5. Reports
- Generate and export in formats like `.html`, `.xml`, `.json`, `.har`:
  - `zap_scan.html`
  - `zap_scan.xml`, etc.
- Provide links in the README or link to your hosted reports.

## Tools & Setup

1. **OWASP Juice Shop**
   - A modern, JavaScript-heavy insecure web application built with Node.js, Express, and Angular. It intentionally includes vulnerabilities from the OWASP Top 10
  
Form Sources- 
1.	Install node.js
2.	Run git clone https://github.com/juice-shop/juice-shop.git --depth 1 (or clone your own fork of the repository)
3.	Go into the cloned folder with cd juice-shop
4.	Run npm install (only has to be done before first start or when you change the source code)
5.	Run npm start
6.	Browse to http://localhost:3000

Docker Container- 
1.	Install Docker
2.	docker pull bkimminich/juice-shop
3.	docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop
4.	Browse to http://localhost:3000 (on macOS and Windows browse to http://192.168.99.100:3000 if you are using docker-machine instead of the native docker installation)

3. **OWASP ZAP (Zed Attack Proxy)**
   - An open-source, flagship OWASP DAST tool with intercepting proxy, traditional + AJAX spiders, passive and active scanning, scripting, and reporting capabilities
4. **Environment**
   - Run Juice Shop locally (via Docker or Node.js) and point ZAP at the target URL (e.g., `http://localhost:3000`) 



## Disclaimer
This project is for **educational and authorized testing purposes only**.  
Do **NOT** run against systems or networks you do not own or have permission to test.

