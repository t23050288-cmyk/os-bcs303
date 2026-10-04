# BCS303 — Dec 2023/Jan 2024 Exam (Set B)
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Define Operating System. Explain dual mode of OS with a neat diagram. [5]

### Definition
An OS is system software that manages computer hardware and lets users run
programs conveniently and efficiently.

### Dual Mode
**Points:**
1. Mode bit distinguishes kernel (0) from user (1) mode.
2. Trap/interrupt/system call switches to kernel mode; privileged instructions
   only run there.

### Diagram
```
 user mode (bit=1): user process executing -> system call -> return from system call
                              |  trap                          ^ return
                              v                                |
 kernel mode (bit=0):              execute system call ---------
```

---

## Q.1 b) Distinguish between the following terms: i) Multiprogramming and Multitasking ii) Multiprocessor system and clustered system. [10]

### (i) Multiprogramming vs Multitasking

| Basis | Multiprogramming | Multitasking |
|---|---|---|
| Goal | Maximize CPU utilization | Fast interactive response |
| Switching trigger | Job waits for I/O | Very frequent timed switching |
| Interaction | Not needed | Direct, interactive |

### (ii) Multiprocessor System vs Clustered System

| Basis | Multiprocessor | Clustered |
|---|---|---|
| Coupling | Tightly coupled (shared bus/memory) | Loosely coupled (separate nodes) |
| Scope | Within one machine | Across networked machines |
| Main benefit | Increased throughput, reliability | High availability |

---

## Q.1 c) With a neat diagram, explain the concept the concept of VM-WARE architecture. [5]

### Definition
VMware abstracts x86 hardware into isolated VMs, running as a user-level
application on a host OS.

### Diagram
```
 application   application    application
     |              |              |
 [guest OS: FreeBSD] [guest OS: WinNT] [guest OS: WinXP]
 ---------------------------------------------------------
                 virtualization layer
 ---------------------------------------------------------
            host operating system (Linux)
 ---------------------------------------------------------
       hardware: CPU | memory | I/O devices
```

---

## Q.2 a) Explain the operating system services with respect to programs and users. [5]

### Points
1. **Program Execution** — load, run, terminate programs.
2. **I/O Operations** — transfer data to/from devices.
3. **File-System Manipulation** — create/delete/search files.
4. **Communications** — IPC between processes.
5. **Error Detection** — hardware/I/O/program error handling.
6. **User Interface** — CLI/GUI/batch for user commands.

---

## Q.2 b) List and explain the different computing environments. [5]

### Points
1. **Traditional/Time-sharing computing** — batch or interactive, CPU-timesliced
   among users.
2. **Client-Server computing** — clients request, servers respond (compute-server
   or file-server).
3. **Peer-to-Peer computing** — all nodes are peers, no fixed client/server role.
4. **Web-based/Cloud computing** — resources delivered over the web (IaaS, PaaS,
   SaaS).
5. **Distributed computing** — networked, physically separate systems sharing
   resources.

---

## Q.2 c) What are system calls? List and explain the different types of system calls. [10]

### Definition
A system call is the interface a process uses to request OS services.

### 6 Types
1. **Process Control** — create/terminate process, allocate memory.
2. **File Management** — create/open/read/write/close files.
3. **Device Management** — request/release device, read/write.
4. **Information Maintenance** — get/set time, system data.
5. **Communications** — send/receive messages, create connections.
6. **Protection** — control access permissions.
