
# CCNA – Network Layer & Address Resolution  
## Communicating between networks

These notes are based on the 20‑question quiz screenshots you shared.  
Each question has the **correct option**, a short **exam explanation**, and a
few **key facts** to remember.

---

## Question 1  
**What IPv4 header field identifies the upper layer protocol carried in the packet?**  

- **Correct answer:** `Protocol`  

**Explanation:**  
The IPv4 header has a **Protocol** field that tells the receiving host which Layer‑4 protocol should handle the payload (for example, TCP = 6, UDP = 17, ICMP = 1). The router does not care about the transport header details, but it forwards the packet while keeping that Protocol value intact.

---

## Question 2  
**What is one advantage that the IPv6 simplified header offers over IPv4?**  

- **Correct answer:** `efficient packet handling`  

**Explanation:**  
The IPv6 header has a **fixed size (40 bytes)** and fewer fields than the IPv4 header. This makes it simpler and faster for routers to process and forward packets, which improves overall packet‑handling efficiency.

---

## Question 3  
**Which field in the IPv4 header is used to prevent a packet from traversing a network endlessly?**  

- **Correct answer:** `Time‑to‑Live (TTL)`  

**Explanation:**  
Every router that forwards a packet **decrements TTL by at least 1**. When TTL reaches 0, the router discards the packet and usually sends an ICMP message back to the source. This prevents routing loops from circulating packets forever.

---

## Question 4  
**Which statement describes a feature of the IP protocol?**  

- **Correct answer:** `IP relies on upper layer services to handle situations of missing or out‑of‑order packets.`  

**Explanation:**  
IP is **connectionless** and **best‑effort**. It does not guarantee delivery, order, or error recovery. Those reliability functions are handled by upper‑layer protocols such as TCP. IP just tries to deliver packets to the destination network.

---

## Question 5  
**What are two services provided by the OSI network layer? (Choose two.)**  

- **Correct answers:**  
  - `routing packets toward the destination`  
  - `encapsulating PDUs from the transport layer`  

**Explanation:**  
Layer 3 (Network layer) encapsulates transport‑layer segments into **packets** and forwards them between networks. Determining the best path and routing those packets are core network‑layer services. Placing frames on the media and collision/error detection are Layer‑2 responsibilities.

---

## Question 6  
**Why is NAT not needed in IPv6?**  

- **Correct answer:**  
  `Any host or user can get a public IPv6 network address because the number of available IPv6 addresses is extremely large.`  

**Explanation:**  
IPv6 uses 128‑bit addresses, which provides an enormous address space. Every device can have a globally unique address, so the original reason for NAT (address conservation) disappears. End‑to‑end addressing becomes normal again.

---

## Question 7  
**How do hosts ensure that their packets are directed to the correct network destination?**  

- **Correct answer:**  
  `They have to keep their own local routing table that contains a route to the loopback interface, a local network route, and a remote default route.`  

**Explanation:**  
Each host maintains a **local routing table**. At minimum this table includes:
- A route to the **loopback** interface,  
- A route for the **directly‑connected local network**, and  
- A **default route** that points toward the default gateway for all remote networks.  

When a host sends a packet, it consults this local table to decide whether the destination is local or should be sent to the default gateway.

---

## Question 8  
**What information does the loopback test provide?**  

- **Correct answer:** `The TCP/IP stack on the device is working correctly.`  

**Explanation:**  
Pinging **127.0.0.1** (or `::1` in IPv6) tests only the local **TCP/IP stack**. If the loopback succeeds, the IP software on the host is operating. It does not test the NIC, cabling, or remote connectivity.

---

## Question 9  
**Which parameter does the router use to choose the path to the destination when there are multiple routes available?**  

- **Correct answer:** `the lower metric value that is associated with the destination network`  

**Explanation:**  
Routing protocols assign a **metric** to each route (for example, hop count, cost, bandwidth). When multiple routes exist to the same destination, the router chooses the route with the **lowest metric** as the best path.

---

## Question 10  
**What is the aim of an ARP spoofing attack?**  

- **Correct answer:** `to associate IP addresses to the wrong MAC address`  

**Explanation:**  
In ARP spoofing/poisoning, an attacker sends forged ARP replies so that devices store **incorrect IP‑to‑MAC mappings** (for example, the gateway IP mapped to the attacker’s MAC). This allows interception or disruption of traffic.

---

## Question 11  
**What statement describes the function of the Address Resolution Protocol (ARP)?**  

- **Correct answer:**  
  `ARP is used to discover the MAC address of any host on the local network.`  

**Explanation:**  
Given a known **IPv4 address**, ARP asks “Who has this IP?” on the LAN (broadcast). The host that owns the address replies with its **MAC address**. ARP operates only inside the local broadcast domain.

---

## Question 12  
**A network technician issues the `arp -d *` command on a PC after the router connected to the LAN is reconfigured. What is the result?**  

- **Correct answer:** `The ARP cache is cleared.`  

**Explanation:**  
`arp -d *` deletes all entries in the host’s **ARP table**. This forces the host to send new ARP requests and learn up‑to‑date MAC addresses, which is useful after topology or gateway changes.

---

## Question 13  
**Which destination address is used in an ARP request frame?**  

- **Correct answer:** `FFFF.FFFF.FFFF` (broadcast MAC address)  

**Explanation:**  
ARP requests are sent as **Layer‑2 broadcasts**. The Ethernet destination MAC is all 1s (`FF‑FF‑FF‑FF‑FF‑FF`) so that every device on the LAN receives the frame and the owner of the IP address can respond.

---

## Question 14  
**PC1 attempts to connect to File_server1 on a remote network and sends an ARP request to obtain a destination MAC address. Which MAC address will PC1 receive in the ARP reply?**  

- **Correct answer:** `the MAC address of the G0/0 interface on R1`  

**Explanation:**  
Because File_server1 is on a **remote network**, PC1 must send the frame to its **default gateway** (R1). PC1 ARPs for the IP address of R1’s G0/0 interface and stores that MAC address. The server’s MAC never appears in PC1’s ARP table.

---

## Question 15  
**Which statement describes the treatment of ARP requests on the local link?**  

- **Correct answer:** `They are received and processed by every device on the local network.`  

**Explanation:**  
ARP request frames are broadcasts. Every NIC on the LAN receives the frame and checks whether the **target IP address** matches its own. Only the matching host replies, but all devices must inspect the request.

---

## Question 16  
**Where are IPv4 address to Layer‑2 Ethernet address mappings maintained on a host computer?**  

- **Correct answer:** `ARP cache`  

**Explanation:**  
The host stores learned IP‑to‑MAC bindings in its **ARP cache** (ARP table). This allows later frames to be sent without broadcasting ARP each time.

---

## Question 17  
**What happens when the `transport input ssh` command is entered on the switch vty lines?**  

- **Correct answer:** `Communication between the switch and remote users is encrypted.`  

**Explanation:**  
On the vty lines, `transport input ssh` restricts remote access to **SSH only**. SSH uses encryption, so management traffic between the administrator and the switch is protected. Telnet is disabled on those lines.

---

## Question 18  
**A router boots and enters setup mode. What is the reason for this?**  

- **Correct answer:** `The configuration file is missing from NVRAM.`  

**Explanation:**  
After loading IOS, the router looks in **NVRAM** for a valid **startup‑configuration** file. If none exists, it starts the **initial configuration dialog (setup mode)** to help create one.

---

## Question 19  
**Which two functions are primary functions of a router? (Choose two.)**  

- **Correct answers:**  
  - `packet forwarding`  
  - `path selection`  

**Explanation:**  
A router’s main Layer‑3 jobs are to determine the **best path** to each destination network (using its routing table) and to **forward packets** out the appropriate interface. Microsegmentation is a switch function; DNS and flow control belong to other layers.

---

## Question 20  
**Match the command with the device mode at which the command is entered.**  

Commands:  
- A. `ip address 192.168.4.4 255.255.255.0`  
- B. `login`  
- C. `copy running-config startup-config`  
- D. `enable`  
- E. `service password-encryption`  

Modes / Prompts:  
- `R1>` – user EXEC mode  
- `R1#` – privileged EXEC mode  
- `R1(config)#` – global configuration mode  
- `R1(config-line)#` – line configuration mode  
- `R1(config-if)#` – interface configuration mode  

**Correct mappings:**  

- **A → `R1(config-if)#`** – IP address commands are entered under interface configuration mode.  
- **B → `R1(config-line)#`** – `login` is configured on console or vty lines.  
- **C → `R1#`** – copying running‑config to startup‑config is a privileged EXEC action.  
- **D → `R1>`** – `enable` is typed in user EXEC to move to privileged EXEC.  
- **E → `R1(config)#`** – `service password-encryption` is a global configuration command.

---

## Question 21  
**Match the phases to the functions during the boot up process of a Cisco router.**  

Phases:  
- Phase 1  
- Phase 2  
- Phase 3  

Functions:  
- perform the POST and load the bootstrap program  
- locate and load the Cisco IOS software  
- locate and load the startup configuration file  

**Correct mapping:**  

- **Phase 1 →** perform the **POST and load the bootstrap program**  
- **Phase 2 →** **locate and load the Cisco IOS software**  
- **Phase 3 →** **locate and load the startup configuration file**  

**Explanation:**  
1. The router powers on, runs **POST**, and loads the **bootstrap** from ROM.  
2. The bootstrap locates and loads the **IOS image**, typically from flash, into RAM.  
3. IOS then looks in **NVRAM** for the **startup‑config** and loads it as the running configuration. If no startup‑config exists, the router enters setup mode.

---

## Question 22  
**What are two functions of NVRAM? (Choose two.)**  

- **Correct answers:**  
  - `to retain contents when power is removed`  
  - `to store the startup configuration file`  

**Explanation:**  
**NVRAM (Non‑Volatile RAM)** keeps its data when the device loses power and is used on Cisco routers and switches to store the **startup‑config**. Routing and ARP tables live in RAM, not NVRAM.

---

## Question 23  
**A network administrator requires access to manage routers and switches locally and remotely. Match the description to the access method.**  

Descriptions:  
- A. unsecure remote access  
- B. remote access method that uses encryption  
- C. preferred out‑of‑band access method  
- D. remote access via a dialup connection  

Access methods:  
- AUX  
- SSH  
- console  
- Telnet  

**Correct mapping:**  

- **A (unsecure remote access) → Telnet** – sends all data, including passwords, in clear text.  
- **B (remote, encrypted) → SSH** – provides encrypted remote management.  
- **C (preferred out‑of‑band) → console** – direct local serial connection to the device.  
- **D (remote via dialup) → AUX** – asynchronous auxiliary port used with modems.

---

## Question 24  
**Match the configuration mode with the command that is available in that mode.**  

Modes:  
- A. `R1(config)#`  
- B. `R1#`  
- C. `R1>`  
- D. `R1(config-line)#`  

Commands:  
- `copy running-config startup-config`  
- `enable`  
- `login`  
- `interface fastethernet 0/0`  

**Correct mapping:**  

- **A (`R1(config)#`) → `interface fastethernet 0/0`** – selecting an interface is done from global configuration mode.  
- **B (`R1#`) → `copy running-config startup-config`** – privileged EXEC command.  
- **C (`R1>`) → `enable`** – used in user EXEC to move into privileged EXEC.  
- **D (`R1(config-line)#`) → `login`** – configured on line (console/vty) modes.

---

## Question 25  
**A new network administrator has been asked to enter a banner message on a Cisco device. What is the fastest way to test whether the banner is properly configured?**  

- **Correct answer:** `Exit privileged EXEC mode and press Enter.`  

**Explanation:**  
The banner is displayed **when a user connects to the device before login**. To test it quickly on the console, the admin can **log out** of the current session (exit from privileged EXEC) and press Enter to start a new login, which will immediately display the banner. Rebooting or power‑cycling would also work but is slower and unnecessary.

---

## Question 26  
**Which three commands are used to set up secure access to a router through a connection to the console interface? (Choose three.)**  

Options included: `enable secret cisco`, `line vty 0 4`, `line console 0`, `interface fastethernet 0/0`, `password cisco`, `login`.  

- **Correct answers:**  
  - `line console 0`  
  - `password cisco`  
  - `login`  

**Explanation:**  
To secure console access you configure the **console line**:

```text
Router(config)# line console 0
Router(config-line)# password cisco
Router(config-line)# login
```

This forces anyone using the console port to enter the specified password. `enable secret` protects privileged EXEC access and `line vty` protects remote (Telnet/SSH) access, not the console itself.

---

## Question 27  
**What are two potential network problems that can result from ARP operation? (Choose two.)**  

- **Correct answers:**  
  - `Network attackers could manipulate MAC address and IP address mappings in ARP messages with the intent of intercepting network traffic.`  
  - `On large networks with low bandwidth, multiple ARP broadcasts could cause data communication delays.`  

**Explanation:**  
- ARP has **no authentication**, so attackers can send fake ARP replies and poison ARP tables, redirecting traffic through their device (man‑in‑the‑middle).  
- ARP requests are **broadcasts**; in very large or low‑bandwidth networks, excessive broadcasts can consume bandwidth and create delays for normal traffic.

---

## Question 28  
**Open the PT activity and determine which interfaces on each router are active and operational.**  

- **Correct answer:**  
  `R1: G0/0 and S0/0/0;   R2: G0/1 and S0/0/0`  

**Explanation:**  
After completing the Packet Tracer activity, only these interface pairs show an **up/up** status on R1 and R2. The other interfaces are either administratively down or do not have proper addressing/clocking configured.

---

## Question 29  
**What is the effect of using the `Router# copy running-config startup-config` command on a router?**  

- **Correct answer:** `The contents of NVRAM will change.`  

**Explanation:**  
`running-config` lives in **RAM**, while `startup-config` is stored in **NVRAM**. This command overwrites the existing startup configuration in NVRAM with the current running configuration. Flash, ROM, and regular RAM contents are not directly changed by this command.

---

## Question 30  
**What will happen if the default gateway address is incorrectly configured on a host?**  

- **Correct answer:** `The host cannot communicate with hosts in other networks.`  

**Explanation:**  
Communication to **remote networks** requires sending packets to the correct **default gateway**. If that IP is wrong, local communication (same subnet) still works, but packets destined for other networks cannot reach the proper router and will fail.

---

## Question 31  
**Which term describes the field in the IPv4 packet header that is used to identify the next level protocol?**  

- **Correct answer:** `protocol`  

**Explanation:**  
The IPv4 **Protocol** field identifies the encapsulated Layer‑4 protocol (for example, TCP, UDP, ICMP). Routers and hosts use this value to hand the payload up to the correct transport‑layer process.

---

## Question 32  
**What property of ARP allows MAC addresses of frequently used servers to be fixed in the ARP table?**  

- **Correct answer:**  
  `A static IP-to-MAC address entry can be entered manually into an ARP table.`  

**Explanation:**  
ARP tables can contain **static entries** configured by the administrator. For important servers, you can manually map their IP address to their MAC address so that the entry does not age out and cannot be changed by normal ARP traffic.

---

## Question 33  
**A network administrator is connecting a new host to the Manager LAN. The host needs to communicate with remote networks. What IP address should be configured as the default gateway on the new host?**  

Given router configuration (simplified):  
- `G0/1` – Registrar LAN: `10.118.63.65 /24`  
- `G0/0` – Manager LAN: `10.118.62.196 /24`  
- `S0/0/0` – ISP: `10.62.63.254 /24`  
- `S0/0/1` – Head Office: `209.165.200.87 /24`  

- **Correct answer:** `10.118.62.196`  

**Explanation:**  
The **default gateway** for hosts on a LAN is the IP address of the **router interface on that same network**. The Manager LAN uses the G0/0 interface with address **10.118.62.196/24**, so that is the address that must be configured as the default gateway on the new Manager LAN host.

---
