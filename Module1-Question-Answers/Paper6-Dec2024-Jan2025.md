# BCS303 — Dec 2024/Jan 2025 Exam
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Define Operating System. Explain dual mode of operating systems with a neat diagram. [6]

### Definition
An OS is system software that manages hardware and provides an environment for
convenient, efficient program execution.

### Dual Mode
**Points:** mode bit (kernel=0, user=1); traps/interrupts/system calls switch to
kernel mode; privileged instructions only run in kernel mode.

### Diagram
```
 user mode (bit=1): user process executing -> system call -> return from system call
                              |  trap                          ^ return
                              v                                |
 kernel mode (bit=0):              execute system call ---------
```

---

## Q.1 b) Distinguish between the following terms: i) Multiprogramming and Multitasking ii) Multiprocessor and Clustered system. [6]

### (i) Multiprogramming vs Multitasking

| Basis | Multiprogramming | Multitasking |
|---|---|---|
| Goal | Maximize CPU utilization | Fast interactive response |
| Trigger for switch | Job waits (I/O) | Frequent timed switching |

### (ii) Multiprocessor vs Clustered

| Basis | Multiprocessor | Clustered |
|---|---|---|
| Coupling | Tightly coupled | Loosely coupled, networked nodes |
| Benefit | Throughput, reliability | High availability |

---

## Q.1 c) Explain with a neat diagram VM-WARE Architecture. [8]

### Definition
VMware abstracts x86 hardware into isolated VMs via a virtualization layer
running on a host OS.

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

### Points
1. Each VM has its own virtual CPU, memory, disk, network interface.
2. Guest OS believes it's running on bare hardware, but is actually inside a
   user-level application.

---

## Q.2 a) List and explain the services provided by OS for the user and efficient operation of system. [6]

### For the user
User Interface, Program Execution, I/O Operations, File-System Manipulation,
Communications, Error Detection.

### For efficient operation
Resource Allocation, Accounting, Protection and Security.

---

## Q.2 b) Explain the different computing equipments [environments]. [6]

### The 5 Computing Environments (each explained)
1. **Traditional / Time-Sharing Computing** — started as batch systems (no
   interaction) and grew into interactive time-sharing, where the CPU rapidly
   cycles among many users so each feels they have their own machine. Modern
   versions add web technology and firewalls.
2. **Client-Server Computing** — clients send requests, servers respond.
   A **compute-server** executes the work (e.g. a database server) and returns
   results; a **file-server** serves files (create/read/update/delete).
3. **Peer-to-Peer (P2P) Computing** — there is no fixed client or server;
   every node is a peer that can both request and provide services. No single
   server bottleneck. Example: BitTorrent file sharing.
4. **Web-Based / Cloud Computing** — computing resources are delivered over
   the Internet instead of run locally: **IaaS** (raw virtual machines),
   **PaaS** (a ready platform to deploy apps), **SaaS** (ready software like
   Gmail).
5. **Distributed Computing** — physically separate computers connected by a
   network (LAN/WAN) that share resources, increasing speed, functionality,
   and reliability.

---

## Q.2 c) What are systems calls? List and explain the different types of systems calls. [8]

### Definition
A system call is the interface a process uses to request a service from the OS.

### 6 Types of System Calls (each explained)
1. **Process Control** — controls how programs run: creating a new process,
   terminating one, waiting for an event, and allocating or freeing memory for
   a program. Example calls: `fork()` to create a child process, `exit()` to
   end a process, `wait()` to wait for a child.
2. **File Management** — all work with files: create, delete, open, close,
   read, write, and change file properties like permissions. Example calls:
   `open()`, `read()`, `write()`, `close()`.
3. **Device Management** — requests and releases hardware devices (disk,
   printer) and reads/writes from them. Example calls: `ioctl()`,
   `read()`, `write()`.
4. **Information Maintenance** — transfers status information between the user
   program and the OS: date, time, process ID, system statistics.
   Example calls: `getpid()`, `time()`, `alarm()`.
5. **Communications** — used for inter-process communication: creating
   connections, sending and receiving messages between processes.
   Example calls: `pipe()`, `send()`, `receive()`.
6. **Protection** — controls which users/processes can access which resources,
   and grants temporary extra permissions when allowed.
   Example call: `chmod()` to change file access permissions.
