# Cryptographic Failures Lab

## Overview

Cryptographic Failures occur when encryption mechanisms fail to properly protect sensitive data.
This may happen due to weak encryption algorithms, improper implementation, or exposure of sensitive data such as password hashes.

In this lab, sensitive data was exposed in a publicly accessible directory, allowing retrieval of a database containing hashed user passwords.

---

## Lab Environment

Platform: TryHackMe
Web Application: Sense and Sensitivity

The application stores sensitive data within the web server directories.

---

## Vulnerability Discovery

While analyzing the web application, a comment was discovered in the page source code suggesting that sensitive data might be stored in a specific directory.

This hint suggested checking the /assets directory.

---

## Exploitation Steps:

## Step 1 — Access the Web Application

Open the provided target address in the browser.

Example:

  **http://10.10.75.201:81**

The page loads the **Sense and Sensitivity application**.

---

## Step 2 — Inspect Page Source

Right-click on the webpage and select View Page Source.

A comment in the source code hints that sensitive data may be stored within the **assets** directory.

---

## Step 3 — Navigate to the Assets Directory

Manually browse to the directory:

  **http://10.10.75.201:81/assets**

The directory listing reveals several files including:

  **webapp.db**

This file appears to contain sensitive application data.

---

## Step 4 — Download the Database File

Download the webapp.db file from the assets directory.

This database contains user account information including hashed passwords.

---

## Step 5 — Extract User Credentials

Open the database using SQLite.

Example command:

  **sqlite3 webapp.db**

Then run the query:

  **SELECT * FROM users;**

This reveals user data including the admin password hash.

---

## Step 6 — Crack the Password Hash

Copy the admin password hash and use an online hash-cracking tool or password cracking service.

After cracking the hash, the plaintext password is obtained.

Example:

Password: qwertyuiop

---

## Step 7 — Login as Admin

Return to the web application login page.

Use the credentials:

  Username: admin
  Password: qwertyuiop

After logging in successfully, the application displays the flag.

**Flag**

THM{Yzc2YjdkMjE5N2VjMzNhOTE3NjdiMjdl}

---

## Impact

**Cryptographic Failures may allow attackers to:**

- Access sensitive data such as passwords

- Retrieve confidential databases

- Compromise administrator accounts

- Gain full control of the application
  
---

## Mitigation

To prevent Cryptographic Failures:

- Avoid storing sensitive data in publicly accessible directories

- Use strong cryptographic algorithms

- Protect sensitive files from direct web access

- Implement proper access control mechanisms

- Store password hashes using strong hashing algorithms

---

## Disclaimer

This documentation describes a lab exercise performed for educational purposes while learning web application security.

---
