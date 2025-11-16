## Scenario: Clicking a new link (https://www.wikipedia.org) when Google.com is already open  
What happens next?

### 1. HTTPS Check → TLS Handshake
The browser notices the URL uses **HTTPS**, so it begins the **TLS handshake**.  
Only after the secure tunnel is created does the browser send the actual HTTP request.

---

### 2. Application Layer
The browser creates the HTTP request:

