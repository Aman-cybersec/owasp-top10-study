# Broken Access Control Lab

## Overview

Broken Access Control occurs when an application fails to properly restrict what authenticated users are allowed to do.
As a result, users can access resources or perform actions outside their intended permissions.

This lab demonstrates how modifying a URL parameter allows unauthorized access to another user's data.

---

## Lab Environment

Platform: TryHackMe
Application: THM Note Server

The lab environment contains a web application that stores user notes.

---

## Vulnerability Description

After logging into the application, the user can view their note through a URL parameter such as:

/note.php?note_id=1

The application directly uses this parameter to retrieve notes from the server without validating whether the user has permission to access that note.

Because of this, changing the **note_id** value allows access to other users' notes.

---

## Exploitation Steps

## Performed in THM

![Broken Access Control Lab](../images/01-broken-access-control.jpg)

### Step 1 — Deploy the machine

Start the lab machine and open the target web application in a browser.

### Step 2 — Login to the application

Use the credentials provided in the lab:

Username: noot
Password: test1234

After login, the THM Note Server dashboard is displayed.

---

### Step 3 — Observe the URL parameter

After login the URL contains a parameter:

/note.php?note_id=1

This parameter determines which note is displayed.

---

### Step 4 — Modify the parameter

Manually change the **note_id** value in the browser URL.

Example:

/note.php?note_id=0

or

/note.php?note_id=2

---

### Step 5 — Access another user's data

After modifying the ID parameter, the application displays notes belonging to another user.

This confirms that the application does not properly enforce access control.

---

### Step 6 — Capture the flag

By accessing another user's note, the flag becomes visible:

flag{fivefourthree}

Submit the flag to complete the lab.

---

## Impact

Broken Access Control vulnerabilities may allow attackers to:

* Access sensitive data
* Modify or delete other users' resources
* Escalate privileges within the application

---

## Mitigation

To prevent Broken Access Control vulnerabilities:

* Enforce **server-side authorization checks**
* Validate user permissions for every request
* Avoid relying on client-side controls
* Implement centralized access control mechanisms

---

## Disclaimer

This write-up is for educational purposes and documents a lab exercise completed while learning web application security.

