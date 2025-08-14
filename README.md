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
2. **OWASP ZAP (Zed Attack Proxy)**
   - An open-source, flagship OWASP DAST tool with intercepting proxy, traditional + AJAX spiders, passive and active scanning, scripting, and reporting capabilities
3. **Environment**
   - Run Juice Shop locally (via Docker or Node.js) and point ZAP at the target URL (e.g., `http://localhost:3000`) 

## Testing Methodology

### 1. Spidering
- **Traditional Spider**: Crawls through hyperlinks to map site structure.
- **AJAX Spider**: Handles JavaScript-heavy or single-page applications by discovering dynamically loaded content via AJAX calls.

### 2. Scanning
- **Passive Scanning**  
  - Listens and analyzes HTTP traffic without sending malicious payloads.
  - Identifies issues like missing headers, information leakage, etc.
- **Active Scanning**  
  - Sends crafted malicious requests to identify deeper vulnerabilities.
  - Should be run **only** in a safe, test environment (like a local Juice Shop instance).

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
- Attempt accessing restricted resources without proper permissions.

### 3f. Denial of Service (DoS)
- Identify endpoints susceptible to resource exhaustion.

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

