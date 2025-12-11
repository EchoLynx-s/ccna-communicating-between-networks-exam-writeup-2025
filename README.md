
# CCNA – Network Layer & Address Resolution  
## Communicating between networks

These notes are based on the 20‑question quiz screenshots you shared.  
Each question has the **correct option**, a short **exam explanation**, and a
few **key facts** to remember.

---

## Question 1  
**What IPv4 header field identifies the upper layer protocol carried in the packet?**

- **Correct answer:** `Protocol`  

**Why?**  
The IPv4 header includes a **Protocol** field (1 byte) that tells the
receiving host which **Layer 4** protocol should process the payload
(e.g., TCP = 6, UDP = 17, ICMP = 1).  

**Key facts**

- IPv4 **Version** = IP version (4).  
- **Identification** = used with fragmentation.  
- **Differentiated Services (DSCP/ECN)** = QoS markings.  
- **Protocol** = maps the packet to TCP/UDP/ICMP/etc.

---

## Question 2  
**What is one advantage that the IPv6 simplified header offers over IPv4?**

- **Correct answer:** `efficient packet handling`  

**Why?**  
The IPv6 header has a **fixed length (40 bytes)** and fewer fields than
IPv4, which simplifies processing in routers. That leads to **more
efficient packet handling and forwarding**.  

**Key facts**

- IPv6 header: fixed size, no checksum, no fragmentation in‑header.  
- Address size is larger, not smaller.  
- Checksum processing is removed, not just “little requirement”.

---

## Question 3  
**Which field in the IPv4 header is used to prevent a packet from traversing a network endlessly?**

- **Correct answer:** `Time‑to‑Live` (TTL)  

**Why?**  
Each router that forwards a packet **decrements TTL by at least 1**.  
When TTL reaches **0**, the packet is discarded and an ICMP message is
usually sent back. This prevents routing loops from circulating packets
forever.  

**Key facts**

- TTL is an 8‑bit field (0–255).  
- In IPv6, the equivalent field is **Hop Limit**.

---

## Question 4  
**Which statement describes a feature of the IP protocol?**

- **Correct answer:** `IP relies on upper layer services to handle situations of missing or out‑of‑order packets.`  

**Why?**  
IP is **connectionless** and **best‑effort**. It doesn’t guarantee
delivery, order, or error recovery. Those functions are handled by
upper‑layer protocols, typically **TCP**.  

**Key facts**

- IP encapsulation does **not** change based on media.  
- Error control and MAC addressing are handled at **Layer 2**.

---

## Question 5  
**What are two services provided by the OSI network layer? (Choose two.)**

Options included: placement of frames on media, routing packets, encapsulating PDUs from transport, error detection, collision detection.  

- **Correct answers:**  
  - `routing packets toward the destination`  
  - `encapsulating PDUs from the transport layer`  

**Why?**  
The **Network layer (Layer 3)** is responsible for:
- **Encapsulating** transport‑layer segments into **packets** (or datagrams).  
- **Routing** those packets between networks to their destination.  

Placement of frames on media, collision detection, and most error
detection are **Layer 2** responsibilities.

---

## Question 6  
**Why is NAT not needed in IPv6?**

- **Correct answer:**  
  `Any host or user can get a public IPv6 network address because the number of available IPv6 addresses is extremely large.`  

**Why?**  
IPv6 provides a **huge global address space** (128‑bit), so every device
can have a **unique public address**. This removes the original
motivation for NAT (address conservation).  

**Key facts**

- NAT can still be used for other reasons (e.g., policy), but **not for
address shortage**.  
- IPv6 was designed to restore true **end‑to‑end addressing**.

---

## Question 7  
**How do hosts ensure that their packets are directed to the correct network destination?**

Options (simplified): query the gateway, maintain complex routing table, search local table and pass info to gateway, or always send to default gateway.  

- **Correct answer (per Cisco exam wording):**  
  `They always direct their packets to the default gateway, which will be responsible for the packet delivery.`  

**Why?**  
In the NetAcad context, the host relies on the **default gateway router**
to choose the best path. If the destination is local, the gateway isn’t
used; but the exam answer simplifies it to: “send to the **default
gateway**, router takes care of delivery.”  

**Key facts**

- Hosts normally have a default route pointing to the gateway.  
- The router uses its own **routing table** to choose the final path.

---

## Question 8  
**What information does the loopback test provide?**

- **Correct answer:** `The TCP/IP stack on the device is working correctly.`  

**Why?**  
Pinging **127.0.0.1** (or `::1` in IPv6) tests the **local TCP/IP
implementation only**. It doesn’t check the NIC, cabling, or remote
connectivity.  

**Key facts**

- Successful loopback = local IP software is OK.  
- If loopback fails, troubleshoot the **host** itself (IP stack / OS).

---

## Question 9  
**Which parameter does the router use to choose the path to the destination when there are multiple routes available?**

- **Correct answer:** `the lower metric value that is associated with the destination network`  

**Why?**  
Routing protocols associate a **metric** with each route (hop count,
cost, bandwidth, etc.). When multiple routes to the same network exist,
the router prefers the route with the **lowest metric**.  

**Key facts**

- Metric meaning depends on the protocol (e.g., RIP hop count, OSPF
cost).  
- Gateway IP address isn’t used as a tiebreaker until **after** metric,
administrative distance, etc.

---

## Question 10  
**What is the aim of an ARP spoofing attack?**

- **Correct answer:** `to associate IP addresses to the wrong MAC address`  

**Why?**  
In ARP spoofing, an attacker sends **forged ARP replies** so that other
devices map a **legitimate IP** (e.g., default gateway) to the
attacker’s **MAC address**. This enables man‑in‑the‑middle attacks,
traffic redirection, or DoS.  

**Key facts**

- ARP spoofing poisons ARP caches with **false IP–MAC bindings**.  
- Broadcast storms or bogus MAC‑tables are related but not the main goal.

---

## Question 11  
**What statement describes the function of the Address Resolution Protocol (ARP)?**

- **Correct answer:**  
  `ARP is used to discover the MAC address of any host on the local network.`  

**Why?**  
ARP operates only within the **local broadcast domain**. Given a **known
IPv4 address**, it discovers the corresponding **Ethernet MAC address**.  

**Key facts**

- ARP does **not** discover IP addresses.  
- Routers do not forward ARP broadcasts to other networks.

---

## Question 12  
**A network technician issues the `arp -d *` command on a PC after the router that is connected to the LAN is reconfigured. What is the result?**

- **Correct answer:** `The ARP cache is cleared.`  

**Why?**  
`arp -d *` deletes **all entries** from the local ARP table. This forces
the host to **re‑ARP** and learn updated MAC addresses, which is useful
after topology or gateway changes.  

**Key facts**

- `arp -a` displays ARP cache.  
- Clearing ARP can fix stale mappings after network changes.

---

## Question 13  
**Which destination address is used in an ARP request frame?**

- **Correct answer:** `FFFF.FFFF.FFFF` (the Ethernet broadcast MAC address)  

**Why?**  
An ARP request is a **Layer 2 broadcast** frame so that **all hosts on
the LAN** receive it and the one with the matching IPv4 address can
reply.  

**Key facts**

- The IPv4 destination in the ARP payload is the **target IP**.  
- The Ethernet destination MAC is `FF:FF:FF:FF:FF:FF`.

---

## Question 14  
**PC1 attempts to connect to File_server1 on a remote network and sends an ARP request to obtain a destination MAC address. Which MAC address will PC1 receive in the ARP reply?**

Topology: PC1 → S1 → R1 → R2 → S2 → File_server1  

- **Correct answer:** `the MAC address of the G0/0 interface on R1`  

**Why?**  
For a **remote destination**, PC1 must send the frame to its **default
gateway** (R1). Thus PC1 ARPs for the **MAC of R1 G0/0**, not for the
server itself. The ARP reply comes from **R1**, and File_server1’s MAC
never appears in PC1’s ARP cache.  

**Key facts**

- Hosts ARP for:
  - **local host** MAC if destination is on same network, or  
  - **gateway** MAC if destination is remote.

---

## Question 15  
**Which statement describes the treatment of ARP requests on the local link?**

- **Correct answer:**  
  `They are received and processed by every device on the local network.`  

**Why?**  
ARP requests are **broadcast frames**, so every NIC on the LAN receives
and passes them to the IP stack. Only the host whose IP address matches
the target IP generates an **ARP reply**, but all devices “process” the
request to check that.  

**Key facts**

- Switches **flood** broadcasts out all ports in the VLAN.  
- Routers **do not forward** ARP broadcasts.

---

## Question 16  
**Where are IPv4 address to Layer 2 Ethernet address mappings maintained on a host computer?**

- **Correct answer:** `ARP cache`  

**Why?**  
The host stores learned IP–MAC bindings in its **ARP cache** (also
called ARP table). This allows future frames to be sent without
re‑broadcasting ARP each time.  

**Key facts**

- On Windows, `arp -a` shows the cache.  
- A switch’s **MAC address table** is different: it maps **MAC → port**.

---

## Question 17  
**What happens when the `transport input ssh` command is entered on the switch vty lines?**

- **Correct answer:**  
  `Communication between the switch and remote users is encrypted.`  

**Why?**  
`line vty 0 4` + `transport input ssh` restricts remote access to **SSH
only** (no Telnet). SSH provides **encrypted** remote management
sessions.  

**Key facts**

- You must also configure:
  - device hostname & domain name  
  - RSA keys (`crypto key generate rsa`)  
  - local usernames / authentication.  

---

## Question 18  
**A router boots and enters setup mode. What is the reason for this?**

- **Correct answer:** `The configuration file is missing from NVRAM.`  

**Why?**  
If the router finds **no valid startup‑config** in NVRAM at boot, it
launches the **initial configuration dialog (setup mode)** to help you
create one.  

**Key facts**

- Missing or corrupt **IOS image** gives different errors (ROMmon, etc.).  
- POST hardware failures also have their own messages, not setup mode.

---

## Question 19  
**Which two functions are primary functions of a router? (Choose two.)**

Options: microsegmentation, domain name resolution, packet forwarding, path selection, flow control.  

- **Correct answers:**  
  - `packet forwarding`  
  - `path selection`  

**Why?**  
Routers operate at **Layer 3**, where their main roles are to:
- **Determine the best path** (path selection) using the routing table.  
- **Forward packets** out the appropriate interface.  

Other items:

- Microsegmentation is a **switch** function.  
- Domain name resolution is **DNS**, an application‑layer service.  
- Flow control is typically handled by **TCP** or data‑link mechanisms.

---

## Question 20  
**Match the command with the device mode at which the command is entered.**

Commands (Categories):

- A. `ip address 192.168.4.4 255.255.255.0`  
- B. `login`  
- C. `copy running-config startup-config`  
- D. `enable`  
- E. `service password-encryption`  

Prompts (Options):

- `R1>` – user EXEC mode  
- `R1#` – privileged EXEC mode  
- `R1(config)#` – global configuration mode  
- `R1(config-line)#` – line configuration mode  
- `R1(config-if)#` – interface configuration mode  

**Correct mappings**

- **A → `R1(config-if)#`**  
  - `ip address ...` is configured under **interface configuration mode**.  
- **B → `R1(config-line)#`**  
  - `login` on its own is used under **line configuration** (console or vty).  
- **C → `R1#`**  
  - `copy running-config startup-config` is a **privileged EXEC** command.  
- **D → `R1>`**  
  - `enable` is entered in **user EXEC** mode to move to privileged EXEC.  
- **E → `R1(config)#`**  
  - `service password-encryption` is a **global configuration** command.  

**Key prompt → mode map**

- `R1>` : user EXEC  
- `R1#` : privileged EXEC  
- `R1(config)#` : global config  
- `R1(config-line)#` : line config  
- `R1(config-if)#` : interface config

---
---

## Question 21 – Cisco Router Bootup Phases

> **Question:**  
> Match the phases to the functions during the boot up process of a Cisco router.

**Correct matching**

- **Phase 1 →** perform the **POST and load the bootstrap program**  
- **Phase 2 →** **locate and load the Cisco IOS software**  
- **Phase 3 →** **locate and load the startup configuration file**

---

### Why this is correct

When a Cisco router powers on, it follows a 3-phase boot sequence:

1. **Phase 1 – POST + Bootstrap**
   - The router runs **Power-On Self-Test (POST)** to check basic hardware (CPU, RAM, interfaces, etc.).
   - Then it loads the **bootstrap program** from ROM.
   - If POST fails, the router can’t continue booting.

2. **Phase 2 – Locate & load the IOS**
   - The bootstrap program looks for a valid **Cisco IOS image**, normally in **flash memory**.
   - If it can’t find IOS in flash, it may try other locations (TFTP, ROMMON, etc.).
   - Once found, the IOS is **decompressed into RAM and executed**.

3. **Phase 3 – Locate & load the startup-config**
   - With IOS running, the router searches **NVRAM** for the **startup-configuration file**.
   - If it **finds** one, it loads it into **running-config** and applies all settings (hostnames, passwords, interfaces, routing, etc.).
   - If it **doesn’t find** one, the router enters **setup mode** (the initial configuration dialog).

---

### Quick memory hook

- **1 – POST & Bootstrap** → _“Am I alive and can I start?”_  
- **2 – Load IOS** → _“Get my operating system.”_  
- **3 – Load startup-config** → _“Apply my personality (config).”_

---
