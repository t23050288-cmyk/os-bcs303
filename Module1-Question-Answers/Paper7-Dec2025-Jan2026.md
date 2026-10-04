# BCS303 — Dec 2025/Jan 2026 Exam
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Explain the various types of system calls with an example for each. [8]

### Definition
A system call is the interface a process uses to request a service from the OS.

### 6 Types with Examples

| Category | Example call | Example use |
|---|---|---|
| Process Control | `fork()` | Create a new child process |
| File Management | `open()` | Open a file for reading |
| Device Management | `ioctl()` | Configure a device |
| Information Maintenance | `getpid()` | Get current process ID |
| Communications | `pipe()` | Create an IPC channel between processes |
| Protection | `chmod()` | Change a file's access permissions |

---

## Q.1 b) Explain cloud computing its types and their services it offers. [8]

### Definition
Cloud computing delivers computing resources (storage, processing power,
software) as a service over the Internet, instead of running them on local
hardware.

### 3 Types ("as-a-Service" model)
1. **IaaS (Infrastructure as a Service)** — raw virtualized hardware (VMs,
   storage, networking) rented from a provider, e.g. AWS EC2.
2. **PaaS (Platform as a Service)** — a managed platform (OS + runtime) for
   deploying apps without managing underlying servers.
3. **SaaS (Software as a Service)** — complete ready-to-use applications
   delivered over the web, e.g. Gmail, Office 365.

### Points
1. Built on top of clustered/virtualized systems for scalability.
2. Benefits: no upfront hardware cost, elastic scaling, pay-as-you-go.

---

## Q.1 c) What is dual mode operation and what is the need of it? [4]

### Definition
Dual-mode operation uses a hardware mode bit to distinguish OS execution (kernel
mode) from user program execution (user mode).

### Need for it
1. Protects the OS from errant/malicious user programs.
2. Protects users from each other.
3. Ensures only the OS can execute privileged instructions (I/O control, timer
   management) — without this, any user program could directly manipulate
   hardware and crash the system.

---

## Q.2 a) Explain the different architecture of OS starting from Simple Structure, Layered Structure, Micro Kernels, Modules and Hybrid Systems. [8]

### 1. Simple Structure
No clear separation of layers (e.g. MS-DOS) — apps can access hardware directly,
risking total system crashes from a single buggy app.

### 2. Layered Structure
OS split into layers, each using only lower layers' services. Simplifies
debugging; less efficient since calls to hardware pass through every layer.

### 3. Microkernels
Minimal kernel (process/memory mgmt + IPC); other services run as user-space
programs, communicating via message passing. Easier to extend; message-passing
overhead reduces performance.

### 4. Modules
Small core kernel + dynamically loadable modules that call each other directly
(no message-passing needed). Used by Solaris, Linux, macOS.

### 5. Hybrid Systems
Most modern OSes (Linux, Windows, macOS) combine ideas from multiple structures
rather than following one pure model.

---

## Q.2 b) Discuss the essential properties of the following types of systems: i. Time sharing system ii. Multi-programmed batch systems. [12]

### i. Time Sharing System
1. CPU switches among multiple users' processes so fast each feels they have a
   dedicated machine.
2. Requires an interactive system; response time typically under 1 second.
3. Uses a timer + scheduling algorithm to cycle through processes.

### ii. Multi-Programmed Batch System
1. Multiple batch jobs kept in memory simultaneously; no user interaction.
2. The OS picks a job and runs it until it needs to wait, then switches to
   another ready job — keeps the CPU busy.
3. Optimizes resource (CPU/I/O) utilization but doesn't provide interactive
   response.
