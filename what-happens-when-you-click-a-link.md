```md
## Scenario: Clicking a new link (https://www.wikipedia.org) when Google.com is already open  
What happens next?

### 1. HTTPS Check → TLS Handshake
The browser notices the URL uses **HTTPS**, so it begins the **TLS handshake**.  
Only after the secure tunnel is created does the browser send the actual HTTP request.

---

### 2. Application Layer
The browser creates the HTTP request:

```

GET / HTTP/1.1
Host: [www.wikipedia.org](http://www.wikipedia.org)

```

It knows what to send because the URL provides the **domain** and **protocol**.  
If HTTPS is used, the request waits until the TLS tunnel is fully established.

---

### 3. Presentation Layer
This layer **translates** the HTTP message into a network-readable format.  
It also performs **encryption** for HTTPS (TLS encryption happens here).

---

### 4. Session Layer
Responsible for opening and maintaining the session between:
- your device  
- the Wikipedia server  

For HTTPS, it helps manage the **TLS handshake** and **session establishment**.

---

### 5. Transport Layer
Adds **source and destination port numbers**:

- Source Port: a random high port (e.g., 513982)  
- Destination Port: **443** (HTTPS)  
- Protocol: **TCP** for reliability

This ensures the data reaches:
- the correct application on the server  
- the correct browser tab on your device

---

### 6. Network Layer
Adds **source and destination IP addresses**.

If the IP is not already cached, DNS resolves it:

```

[www.wikipedia.org](http://www.wikipedia.org) → 208.80.154.224

```

Now an IP packet is formed:

- Source IP: your laptop’s IP  
- Destination IP: 208.80.154.224  

---

### 7. Data Link Layer
Adds the Ethernet **header and trailer**.

If the MAC address of the next hop (usually your router) is unknown, **ARP** is used.

Ethernet frame:

- Source MAC: your NIC’s MAC  
- Destination MAC: router’s MAC  

---

### 8. Physical Layer
The frame is converted to **bits** and sent over the medium (wired or Wi-Fi radio signals).
```

