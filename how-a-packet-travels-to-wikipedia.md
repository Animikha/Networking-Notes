## What happens at the Data Link and Network Layer when you click a new link (https://www.wikipedia.org)?

When you click a new link, your device must start a new connection. At the **Data Link Layer**, it creates an Ethernet frame:

- **Source MAC:** your device’s MAC  
- **Destination MAC:** your router’s MAC  

If your device does not already know the router’s MAC, it performs **ARP**:

1. Your device sends an ARP request: *“Who has this IP (the gateway IP)?”*  
2. The switch **broadcasts** this request to all ports.  
3. Every device ignores it except the router.  
4. The router replies with its MAC address.  
5. The switch forwards the reply back to your device.  

Now your device knows the router’s MAC.

---

## Sending the Packet

Once ARP is done, your device can send the actual **HTTP/TCP/IP** packet.

- The router receives the frame  
- Strips the **Layer 2 header**  
- Checks the **destination IP** (the IP of wikipedia.org)  
- Looks up the next hop in its routing table  

The router then creates a new Ethernet frame:

- **Source MAC:** router’s own MAC  
- **Destination MAC:** next-hop router’s MAC  

Every router along the path repeats this process:
- Examine IP header  
- Determine next hop  
- Replace Ethernet (Layer 2) header  
- Forward the frame  

This continues **hop-by-hop** across the network.

---

## CDN Behavior

The packet usually doesn’t go to the main “Wikipedia server.”  
It typically reaches a **CDN (Content Delivery Network) edge node**.

For Wikipedia (Wikimedia), traffic from India usually goes to:
- **Singapore POP**, or  
- **Amsterdam POP**

These are edge caching servers, not the original backend servers.

---

## Overall Path
PC → Switch → Home Router → ISP Network → Internet Backbone → CDN/Edge Router → CDN Cache Server (or Origin Server if uncached)
