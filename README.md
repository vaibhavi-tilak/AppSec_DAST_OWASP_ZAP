# AppSec_DAST_OWASP_ZAP
# OWASP Juice Shop Security Assessment with OWASP ZAP- a DAST tool

## Overview
This project demonstrates a **Comprehensive Web Application Security Assessment** of the intentionally vulnerable **OWASP Juice Shop** using **OWASP ZAP** for Dynamic Application Security Testing (DAST).

### Objectives
- Explore web crawling techniques: **traditional spidering** and **AJAX crawling**
- Perform **passive scanning** as well as **active vulnerability scanning**
- 
- Identify key vulnerabilities including:
    - **Broken access control**
- Generate downloadable scan reports and link to them

### Tools & Setup: 
https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/SetupREADME.md

> **Note:** Run OWASP Juice Shop **locally** (via Node.js or Docker) for testing purposes.  
> Do **NOT** send automated scans, fuzzing, or exploit requests to the public OWASP Juice Shop demo website, as it is shared by other users and may cause disruption.  
> Always perform security testing only in your own isolated lab environment


## Testing Methodology

### 1. Spidering
- **Traditional Spider**: Crawls through hyperlinks to map site structure.
  
Navigate to:  ```Tools--> Spider```

  ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/2.1%20Spider.png)

- **AJAX Spider**: Handles JavaScript-heavy or single-page applications by discovering dynamically loaded content via AJAX calls.
  
Navigate to: ```Tools--> AJAX Spider```

![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/2.%20AJAX%20Spider.png)


- Apart from this we can use following types of scans
  ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/3.%20Types%20of%20Attacks.png)
  
## 2. Scanning
- **Passive Scanning**  
  - Listens and analyzes HTTP traffic without sending malicious payloads.
  - Identifies issues like missing headers, information leakage, etc.
  
  Navigate to:  ```Manual Explore```
  ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/4.%20Passive.png)
  
  ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/4.1%20Passive%20Scan%20Rules.png)
  
- **Active Scanning**  
  - Sends crafted malicious requests to identify deeper vulnerabilities.
  - Should be run **only** in a safe, test environment (like a local Juice Shop instance).
    
    Navigate to: ```Automate Explore```
    
    ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/3.1%20Attack%20Options.png)

## 3 Scan Policy Manager:

- The Scan Policy Manager in OWASP ZAP is a powerful feature that allows you to customize how active scans are performed by managing scanning rules and their behavior. Three key configurable settings in the Scan Policy Manager are Threshold, Strength, and Status.
- ![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/7.%20Scan%20Policy%20Manager.png)

-a. Threshold : Threshold controls how likely ZAP is to report potential vulnerabilities during a scan. It determines the sensitivity level of the scan rules.
-Possible Threshold values:
- Off: The scan rule is disabled and won't run.
- Low: More potential issues are flagged, increasing the chances of false positives.
- Medium (default): Balanced level to flag likely issues.
- High: Fewer issues are flagged, reducing false positives but may miss some vulnerabilities.

-b. Strength : Strength controls the intensity and number of attack requests ZAP sends for each scanning rule.It determines how thorough the scan is in attacking the target.
- Possible Strength values:
- Low: Fewer attacks, quicker scan, but may miss issues.
- Medium (default): Balanced attack intensity.
- High: More attacks, finds more issues but slower scan.
- Insane: Maximum attack intensity, used for small areas like login pages, very thorough but takes a long time.

-c. What is Status in Scan Policy Manager?
- Status determines if a scan rule is enabled or disabled.
- Common statuses used in ZAP include:
- Release: Stable and fully enabled scan rules.
- Beta or Alpha: Experimental or less stable rules that can be optionally enabled.

    ![imagage_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/7.2%20Scan%20Policy.png)

## 4. Additional Manual Vulnerabilities Tested

In this project, we conducted comprehensive security testing to identify various vulnerabilities within the application. Each identified vulnerability has been carefully mapped to the corresponding OWASP Top 10 category. For every vulnerability, we have detailed the technical cause explaining how the issue arises, classified it under the appropriate category, and outlined mitigation strategies based on the official OWASP guidelines. This structured approach ensures a clear understanding of the risks and provides actionable recommendations to enhance the application's security posture effectively.

https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/Juice%20Shop%20Vulnerabilities.xlsx


### 4a. Broken Access Control
**Definition:**  
Broken Access Control occurs when applications fail to enforce permissions properly, allowing unauthorized users to access restricted data or functions.

**Steps Taken:**  
1. Created a regular user account in Juice Shop.  
2. Configured OWASP ZAP as an intercepting proxy to capture HTTP requests.  
3. Intercepted the registration request containing a JSON body with `"role": "customer"`. Right Click on the request-> Open/Resend with Request Editor->
4. Add "role":"admin" and modify email address.

![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/Manual%20Request%20Editor-%20Role%20email%20change.png)
![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/BOLA%20Success.png)

**Result:**  
- The server accepted the modified request without validation.  
- The new user account was created with **administrator privileges**, granting access to all admin functionalities.  

**Key Takeaway:**  
Servers must **never trust client-supplied role or permission data**. Always enforce role-based access control at the server side.

---



## 5. Reports
1. In the ZAP main menu, go to Report → Generate Report… or click the "Generate Report" toolbar button.
2. In the Generate Report dialog, configure the report options: Enter a title for the report.
3. Choose the filename and directory for saving the report.
4. Optionally, select specific contexts or sites to include in the report.
5. Choose a template for the report format such as HTML, MD, PDF, JSON, or XML.
6. Use filters to include alerts based on risk level and confidence.
7. Optionally include or exclude sections of the report depending on the template.
8. Click Generate Report. ZAP will create the report file in the selected format and save it to the chosen location.

-![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/5.png)

-![image_alt](https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/5.1%20Report%20Generation.png)

- Reports:

- Passive Scan: https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/Passive%20Scan%20-%20Manual%20JuiceShop%20Report.pdf

- Active Scan: https://github.com/vaibhavi-tilak/AppSec_DAST_OWASP_ZAP/blob/main/1/Active%20Scan%20-%20Automated%20Scan%20JuiceShop.pdf

## Disclaimer
This project is for **educational and authorized testing purposes only**.  
Do **NOT** run against systems or networks you do not own or have permission to test.

