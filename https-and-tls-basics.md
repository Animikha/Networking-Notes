# My Idea of HTTPS / TLS (Basics)

## HTTP 

HTTP stands for **HyperText Transfer Protocol**.
It is an application-layer protocol used for communication between clients and servers over the internet.
 A client (usually a browser) sends an HTTP request such as:

 ```http
 GET /index.html HTTP/1.1
 Host: example.com
 ```

 The server then responds with the requested data such as:
 - HTML pages
 - JSON 
 - images
 - videos
 - files

 Originally, "hypertext" referred to linked web documents/websites

  ---

## Problem with HTTP
HTTP traffic is not encrypted.
This means data is transmitted in plaintext.

Althouh all network communication ultimately travels as binary data (bits), the 
contents are still readable as they ae not encrypted. Tools like packet sniffers
can reconstruct and read the original conversation.

Because of this:
- attackers can intercept traffic
- passwords can be stolen
- data can be modified in transit
- websites can be potentially impersonated

HTTP also does not provide strong uthenication of the sserver's identity


## HTTPS
HTTPS stands for **HyperText Transfer Protocol Secure**

It is essentially:
> HTTP runnning over TLS (Transport Layer Security)

People often say "SSL", but moderm HTTPS actually uses **TLS**. SSL is the older, deprecated version.

HTTPS provides:
1. Encryption
2. Authentication
3. Integrity

---

## TLS Certificates
HTTPS uses TLS certificates to verify the identity of the server.

A TLS certificate contains:
- the domain name
- the server's public key
- certificate issuer information
- validity/expiry dates
- a digital signature from a trusted Certificate Authority (CA)

Examples of Certificate Authorities:
- Digicert
- Let's Encrypt

---
Deeper dive into Modern TLS in tls-1.3.basics.md


