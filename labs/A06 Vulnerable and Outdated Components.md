# Vulnerable and Outdated Components Lab

## Overview

Vulnerable and Outdated Components occur when applications use libraries, frameworks, or software components that contain known security vulnerabilities or are no longer supported.

Attackers can exploit these outdated components to gain unauthorized access, execute remote code, or compromise the entire system.

This lab demonstrates how an attacker can identify a vulnerable web application version and use a public exploit to gain remote code execution.

---

## Lab Environment

Platform: TryHackMe  
Application: Online Book Store 1.0

The target web application is running an outdated version of an online bookstore application that contains a known vulnerability.

---

## Vulnerability Description

The application is built using outdated components that contain publicly known vulnerabilities.

By searching vulnerability databases such as **Exploit-DB**, attackers can find exploits targeting the specific application version.

In this lab, **Online Book Store 1.0** has an **Unauthenticated Remote Code Execution (RCE)** vulnerability that allows an attacker to upload a malicious web shell and execute commands on the server.

---

## Exploitation Steps

## Performed in THM

![Vulnerable and Outdated Components Lab](../images/02-vulnerable-outdated-comp.jpg)

### Step 1 — Deploy the machine

Start the TryHackMe lab machine and obtain the target IP address.

Open the target application in a browser.

Example:


http://10.10.136.255:84


The web page displays the **Online CSE Bookstore** application.

---

### Step 2 — Identify the application version

From the web page information, the application version is identified as:


Online Book Store 1.0


This indicates that the application might contain known vulnerabilities.

---

### Step 3 — Search for public exploits

Search for the application in **Exploit-DB**.

Example search:


online book store 1.0


A result appears:


Online Book Store 1.0 - Unauthenticated Remote Code Execution


Download the exploit script.

---

### Step 4 — Execute the exploit

Run the exploit script with the target URL.

Example command:


python3 47887.py http://10.10.61.68:84/


The exploit uploads a **PHP web shell** to the vulnerable server.

---

### Step 5 — Verify shell access

After successful upload, the exploit provides a command shell.

From the shell, execute commands on the server.

Example:


cat /opt/flag.txt


---

### Step 6 — Capture the flag

The flag stored in the system is revealed:


THM{But_1ts_n0t_my_f4ult!}

Submit the flag to complete the lab.

---

## Impact

Using vulnerable or outdated components can allow attackers to:

* Execute remote code on the server
* Upload malicious files
* Gain full system access
* Steal sensitive data
* Compromise the entire application infrastructure

---

## Mitigation

To prevent vulnerabilities caused by outdated components:

* Regularly **update software libraries and frameworks**
* Monitor **security advisories and CVE databases**
* Remove unused dependencies
* Use **automated vulnerability scanning tools**
* Maintain a **software inventory and patch management process**

---

## Disclaimer

This write-up is for educational purposes and documents a lab exercise completed while learning web application security.
