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

These are temporary Diffie-hellman keys

They are deleted after the session ends

--- 

# Step 1 - Browser Connects

User visits:
```text
https://example.com
```

Browser sends:



