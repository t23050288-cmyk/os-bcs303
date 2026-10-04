# BCS303 — Dec 2023/Jan 2024 Exam (Set A)
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Define operating system. Compare multiprogramming and time sharing system. [8]

### Definition
An operating system is system software that acts as an intermediary between a
computer user and the computer hardware.

### Comparison Table

| Basis | Multiprogramming | Time Sharing (Multitasking) |
|---|---|---|
| Goal | Maximize CPU utilization | Fast interactive response |
| Switching frequency | Only when a job waits (e.g. I/O) | Very frequent, rapid switching |
| User interaction | None required | Direct, interactive |
| Response time | Not a concern | Must be short (< 1 sec typically) |
| Relationship | Time sharing is a logical **extension** of multiprogramming | — |

### Points
1. Multiprogramming keeps several jobs in memory so the CPU is never idle.
2. Time-sharing switches the CPU among processes so fast that each user feels
   they have a dedicated machine.

---

## Q.1 b) Describe the structure of operating system and its operations. [7]

### OS Structures (brief)
1. **Simple structure** — no clear separation of layers (e.g. MS-DOS); any
   application can access hardware directly, risking system crashes.
2. **Layered approach** — OS split into layers, each using only the layer below
   it; simplifies debugging but adds overhead since calls must pass through
   every layer down to hardware.
3. **Microkernels** — minimal kernel (process/memory mgmt + IPC); other services
   run as user-space programs communicating via message passing.
4. **Modules** — small core kernel + dynamically-loadable modules that can call
   each other directly (combines layering's clarity with direct-call efficiency).

### OS Operations
1. Modern OSes are **interrupt driven** — they sit idle until an interrupt/trap
   occurs.
2. **Dual-mode operation**: user mode vs kernel mode, enforced via a mode bit.
3. A **timer** ensures the OS always regains control from a runaway program.

---

## Q.1 c) Differentiate Client – Server computing and Peer to Peer computing. [5]

### Comparison Table

| Basis | Client-Server | Peer-to-Peer (P2P) |
|---|---|---|
| Roles | Fixed: client requests, server provides | Any node can be client or server |
| Bottleneck | Server is a bottleneck | No single bottleneck — distributed |
| Service discovery | Client knows the server's address | Centralized lookup OR broadcast discovery |
| Example | Database server, web server | File-sharing networks (e.g. BitTorrent) |

### Points
1. **Compute-server**: handles action requests (e.g. database query).
2. **File-server**: provides file create/read/update/delete interface.
3. P2P nodes must first **join** the network before providing/requesting services.

---

## Q.2 a) Explain various services of operating system. [8]

### Services helpful to the user
1. User Interface (CLI/GUI/batch)
2. Program Execution
3. I/O Operations
4. File-System Manipulation
5. Communications (IPC)
6. Error Detection

### Services for efficient operation
7. Resource Allocation
8. Accounting
9. Protection and Security

---

## Q.2 b) What is system call? Explain all types of system calls. [7]

### Definition
A system call is the interface through which a user program requests OS services.

### 6 Types
1. **Process Control** — create/terminate process, wait/signal event, allocate memory.
2. **File Management** — create/delete/open/close/read/write files.
3. **Device Management** — request/release device, read/write, get/set attributes.
4. **Information Maintenance** — get/set time, system data, process/file attributes.
5. **Communications** — create/delete connection, send/receive messages.
6. **Protection** — adjust access-control mechanisms.

---

## Q.2 c) What are various system programs? Explain. [5]

### Definition
System programs provide a convenient environment for program development and
execution, sitting between the user and raw system calls.

### 6 Categories
1. **File management** — create, delete, copy, rename, list files.
2. **Status information** — date, time, number of users, disk/memory space.
3. **File modification** — text editors.
4. **Programming-language support** — compilers, assemblers, debuggers.
5. **Program loading and execution** — loaders, interactive debuggers.
6. **Communications** — mail, browsers, remote login, file transfer.
