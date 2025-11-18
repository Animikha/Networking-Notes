# Difference between ARP Request and the Switch Flooding its Interfaces due to Unknown Unicast Frames 

These two behaviours look similar (the switch sends the frame out of all interfaces), but the reason and handling are completely different.

---

## Scenario 1: Unknown Unicast Flooding

PC1 wants to send a frame to PC2 which is in the same LAN and knows both its IP address and MAC address. PC1 sends a known unicast frame:

- **Source IP Address:** PC1’s private IP  
- **Destination IP Address:** PC2’s private IP  
- **Source MAC:** PC1’s MAC  
- **Destination MAC:** PC2’s MAC  

When this frame reaches the switch, if the switch does not know which interface PC2 is on, it will flood the frame out of all interfaces except the one it came from. This is called an **unknown unicast**. The switch is **not broadcasting**; it is flooding because it has no entry for PC2 in its MAC table and therefore doesn't known whichinterface PC2 is on.

Only PC2 accepts the frame because the destination MAC matches its own, all the other devices ignore it.

---

## Scenario 2: ARP Request (Broadcast)

PC1 wants to send a frame to PC2 which is in the same LAN but only knows PC2’s IP address, not its MAC address. PC1 therefore sends an ARP Request:

- **Source IP Address:** PC1’s private IP  
- **Destination IP Address:** PC2’s private IP  
- **Source MAC:** PC1’s MAC  
- **Destination MAC:** FF:FF:FF:FF:FF:FF  

When this frame reaches the switch, the switch sees that it is a broadcast frame and sends it out of all interfaces except the one it came from. Every device receives this ARP Request because the destination MAC is broadcast.

Each device checks:

> “Is the ARP target IP equal to my IP?”

Only PC2 finds a match and replies with an ARP Reply:

- **Source IP Address:** PC2’s private IP  
- **Destination IP Address:** PC1’s private IP  
- **Source MAC:** PC2’s MAC  
- **Destination MAC:** PC1’s MAC  

PC1 receives this ARP reply, lerans PC2’s MAC address and stores it in ARP cache, and can now send unicast frames directly to PC2.

