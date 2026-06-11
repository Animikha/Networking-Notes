# TLS 1.3 Handshake 

# What TLS is Trying To Achieve

TLS provides 4 major protections:

| Goal | Meaning |
|---|---|
| Confidentiality | Others cannot read traffic |
| Integrity | Others cannot modify traffic |
| Authentication | Browser verifies it's really `example.com` |
| Perfect Forward Secrecy | Future key leaks shouldn't decrypt old traffic |

---
# Keys Involved

## 1. Server's Long-Term Identity Keys

Server owns:

```text
SERV_PUB
SERV_PRIV
```

- `SERV_PUB` → public key
- `SERV_PRIV` → private key

These identify the server.
`SERV_PUB` is inside the certificate

---

## 2. DigiCert's Keys

DigiCert owns:

```text
DC_PUB
DC_PRIV
```

Browser already trusts:

```text
DC_PUB
```

The server's certificate is already signed by:

```text
DC_PRIV
```

---

### Temporary Ephemeral Keys (Per Connection)

For THIS session only:

```
BROW_EPH_PRIV
BROW_EPH_PUB

SERV_EPH_PRIV
SERV_EPH_PUB
```

These are temporary Diffie-Hellman keys

They are deleted after the session ends

--- 

# Step 1 - Browser Connects

User visits:

```text
https://example.com
```

Browser sends:

```text
ClientHello
```
containing:
- supported TLS versions
- supported cipher suites
- random values
- 'BROW_EPH_PUB`

This public ephemeral value is safe to send openly

---

# Step 2 - Server Responds
Server sends:

```text
ServerHello
```
containing:


## A. Certificate
Certificate contains:

 ```text
- domain: example.com
- SERV_PUB
- issuer: DigiCert
- validity dates
- DigiCert signature
```

Meaning:

```text
"DigiCert confirms this publiec key belongs to example.com"
```

## B. Server's Emphemeral Public Key

Server sends:

```text
SERV_EPH_PUB
```
for Diffie-Hellman's shared secret derivation


## C. Server's Signature

Server signs handshake data using:

```text
SERV_PRIV
```

Browser later verifies this using:

```text
SERV_PUB
```
This proves:

```text
The emphemeral key genuinely came from example.com
```

Without this signature:
Attacker could replace Server's ephemeral key with their own

---

# Step 3 - Browser Verifies Identity

Browser now checks:

## A. DigiCert Signature

Using:

```text
DC_PUB
```
browser verifies DigiVert's signature o the certificate

If valid

```text
Certificate really came from DigiCert
```


### B. Domain Name

Browser checks:

```text
Requested domain = example.com
Certificate domain = example.com
```
Must match


### C. Certificate Validity

Browser checks:

- not expired
- not revoked
- properly formatted

### D. Server's Handshake Signature

Using:

```text
SERV_PUB
```

Browser verifies Server's handshake signature

This proves:

```text
Server really owns SERV_PRIV
```

At this point browser trusts:

```text
"I am talking to the real example.com"
```
---

# Important Point

These private keys NEVER travel across network:

```text
DC_PRIV
SERV_PRIV
BROW_EPH_PRIV
SERV_EPH_PRIV
```

They always remain secret

---

# Step 4 - Shared Session Key is Derived

This is the coe Diffie-Hellman step

The actual:

```text
SESSION_KEY
```

is never transmitted over the network

Instead BOTH sides independently derive the same key

## Browser Computes 

Using:
```text
BROW_EPH_PRIV
+
SERV_EPH_PUB
```

browser derives:

```text
SESSION_KEY
```

## Server Computes

Using:

```text
SERV_EPH_PRIV
+
BROW_EPH_PUB
```

server derives:

```text
SESSION_KEY
```

Due to Diffie-Hellman mathematics:

```text
both derive identical SESSION_KEY
```

without ever sending it across the network

---

# What Attacker can see

```text

```
















