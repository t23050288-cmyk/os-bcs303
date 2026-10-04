# 9. Computing Environments, Distributed Systems & Special-Purpose Systems

Covers: "Explain cloud computing its types and their services it offers",
"Discuss the essential properties of: Time sharing system, Multi-programmed
batch systems", "List and explain the different computing environments",
"Explain the different computing equipments", "What are the different special
purpose systems?".

---

## 9.1 Traditional / Time-Sharing Computing

**Points:**
1. Years ago, systems were either **batch** (jobs processed in bulk with
   predetermined input, no interaction) or **interactive** (waiting on user
   input).
2. **Time-sharing systems** use a timer + scheduling algorithm to rapidly cycle
   the CPU among multiple users' processes — each user gets a "slice" of CPU
   time, giving the illusion of a dedicated machine.
3. **Multi-programmed batch systems**: multiple batch jobs are kept in memory at
   once so the CPU always has something to execute (see file 04, §4.1) — no
   direct user interaction, but higher resource utilization than running one job
   at a time.
4. Modern trend: Web technology stretches traditional computing — companies use
   **portals** for web access to internal servers; **network computers** are
   essentially web-aware terminals; **firewalls** protect home/office networks.

---

## 9.2 Client-Server Computing

**Definition:** As designers moved away from centralized "dumb terminal" systems,
many modern systems now act as **servers** satisfying requests from **client**
systems — a specialized form of distributed system.

**Points:**
1. **Compute-server system**: client sends a request (e.g. "read data"); server
   executes it and returns results. Example: a database server.
2. **File-server system**: provides a file-system interface — clients
   create/update/read/delete files. Example: a web server delivering files to
   browsers.

---

## 9.3 Peer-to-Peer (P2P) Computing

**Definition:** Clients and servers aren't distinguished — all nodes are **peers**,
each acting as either client or server depending on whether it's requesting or
providing a service.

**Points:**
1. In client-server, the server is a **bottleneck** (all requests go through it).
   In P2P, services are distributed across many nodes — no single bottleneck.
2. A node must first **join** the P2P network before it can provide/request
   services.
3. Two ways to discover available services:
   - Register with a **centralized lookup service** when joining; clients query
     this registry to find a provider.
   - **Broadcast** a request for the service to all peers; whichever node(s)
     offer it respond (needs a **discovery protocol**).
4. Example: file-sharing networks like BitTorrent.

---

## 9.4 Web-Based / Cloud Computing

**Points:**
1. Web computing increases the importance of networking — devices that weren't
   networked before now have wired/wireless access.
2. **Load balancers** distribute network connections among a pool of similar
   servers.
3. **Cloud computing** delivers computing resources (storage, processing,
   software) as a service over the Internet rather than running them locally.
4. **Types of cloud services (the common "as-a-Service" model):**
   - **IaaS (Infrastructure as a Service)** — raw virtualized hardware (VMs,
     storage, networking) rented from a provider (e.g. AWS EC2).
   - **PaaS (Platform as a Service)** — a managed platform (OS + runtime)
     for deploying applications without managing the underlying servers.
   - **SaaS (Software as a Service)** — complete ready-to-use applications
     delivered over the web (e.g. Gmail, Office 365).
5. Cloud computing environments are usually built on top of clustered or
   virtualized systems for scalability and resource sharing.

---

## 9.5 Distributed Systems

**Definition:** A distributed system is a collection of physically separate,
possibly heterogeneous computer systems networked together to give users access
to the various resources the system maintains.

**Points:**
1. Benefits: increased computation speed, functionality, data availability, and
   reliability.
2. A **network** is simply a communication path between two or more systems;
   **TCP/IP** is the most common network protocol (basis of the Internet).
3. Networks classified by distance:
   - **LAN (Local-Area Network)** — within a room/building/campus.
   - **WAN (Wide-Area Network)** — links buildings/cities/countries.
   - **MAN (Metropolitan-Area Network)** — links buildings within a city.
   - **PAN (Personal-Area Network)** — e.g. Bluetooth between a phone and
     headset, over just a few feet.
4. **Network operating system**: provides file sharing + a communication scheme
   across the network, but each computer still runs mostly autonomously.
5. **Distributed operating system**: computers communicate closely enough to
   give the illusion that a **single** OS controls the whole network.

---

## 9.6 Special-Purpose Systems

### Multimedia Systems
**Points:**
1. Handle audio/video data in addition to conventional files.
2. Multimedia data (e.g. video frames) must be delivered ("streamed") under
   **time restrictions** — e.g. 30 frames per second — unlike ordinary data,
   which has no such delivery deadline.
3. Examples: MP3 audio, DVD movies, video conferencing, live webcasts.

### Handheld Systems
**Points:**
1. Includes PDAs and smartphones; developers face challenges from **limited
   memory**, **slower processors** (to save battery/power), and **small
   screens**.
2. Memory must be managed very efficiently — unused allocated memory must always
   be returned to the OS.
3. Faster processors need more power, requiring bigger batteries — a direct
   design trade-off for handhelds.
4. Despite these limits, handhelds succeed due to convenience/portability, and
   their utility keeps growing (cameras, media players, network connectivity).
