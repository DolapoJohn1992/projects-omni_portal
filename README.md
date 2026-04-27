Omni-Portal Security Assessment Report
Auditor: Dolapo Adewale John

Date: April 27, 2026

Target: Titan Omni-Portal (Internal Legacy App)

Project Overview
This repository contains a comprehensive security audit of the Titan Omni-Portal system. The assessment focuses on identifying critical vulnerabilities such as SQL Injection and Cross-Site Scripting (XSS) to improve the overall security posture of the application.

Key Findings
1. Breaking the Gate (SQL Injection)

Vulnerability: SQL Injection (SQLi) Tautology.

Payload Used: ' OR 1=1 --.

Result: Successfully bypassed the authentication check without a valid password, gaining unauthorized access to the application dashboard.

2. Poisoning the Well (Stored XSS)

Vulnerability: Stored Cross-Site Scripting (XSS).

Payload Used: <script>alert(document.cookie)</script>.

Result: Demonstrated the ability to inject malicious scripts into the application, which could lead to session hijacking.

Tools Used
Environment: Linux VirtualBox (Ubuntu).

Version Control: Git and GitHub.

Editors: VS Code and Nano.

