# Injection Lab

## Overview

Injection vulnerabilities occur when an application accepts untrusted input and sends it to an interpreter such as a command shell or database without proper validation. Attackers can exploit this by inserting malicious commands that are executed by the system.

In this lab, a command injection vulnerability allows execution of operating system commands through a web application input field.

---

## Lab Environment

Platform: TryHackMe  
Application: Cowsay Online

The application allows users to input text that is processed by a backend command-line program.

---

## Vulnerability Description

The web application does not properly sanitize user input before passing it to a system command. Because of this, attackers can inject additional commands using special characters.

This allows the attacker to execute arbitrary commands on the server.

---

## Exploitation Steps

## 

### Step 1 – Access the Web Application

Open the application in the browser.

http://10.10.35.8:82


The page loads the **Cowsay Online** interface where users can enter text.

---

### Step 2 – Test Input Field

The application accepts user input and displays the result using the Cowsay program.

Example input:

  **Hello**


This confirms that user input is processed by a system command.

---

### Step 3 – Inject a System Command

Insert a command injection payload into the input field. 

$(ls)

This executes the **ls command**, revealing files in the root directory.

A suspicious file appears:

drpepper.txt

---

### Step 4 – Read Sensitive System File

Use command injection to read the system password file.

$(cat /etc/passwd)

This reveals system users running on the server.

Observation:

The application runs under the **apache user**.

---

### Step 5 – Check Operating System Information

Execute another command to reveal the OS version.

$(cat /etc/os-release)

Output reveals:

**Alpine Linux 3.16**

---

### Step 6 – Answer Lab Questions

From the command outputs we determine:

Strange text file in root directory: drpepper.txt


Number of non-root / non-service users: 0


User running the application: apache


User shell: /sbin/nologin


Operating system version: Alpine Linux 3.16.0

---

## Impact

Injection vulnerabilities may allow attackers to:

- Execute arbitrary system commands
- Access sensitive system files
- Discover server configuration
- Escalate privileges
- Fully compromise the server

---

## Mitigation

To prevent injection vulnerabilities:

- Validate and sanitize all user inputs
- Use parameterized queries or safe APIs
- Avoid executing system commands with user input
- Implement Web Application Firewalls (WAF)
- Restrict user permissions on the server

---

## Disclaimer

This repository documents cybersecurity labs completed for educational purposes while learning web application security concepts.

