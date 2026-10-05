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

### 5 Computing Environments
1. **Traditional / Time-Sharing Computing**:
   Evolved from batch processing to interactive time-sharing systems where a central CPU rapidly cycles among multiple users to give the illusion of dedicated computers. Modern traditional computing incorporates web technology, connecting PCs to company servers behind network firewalls.
2. **Client-Server Computing**:
   Specialized network architecture where client nodes send service requests to server nodes. Servers are categorized as compute-servers (executing computations like database searches and sending back results) or file-servers (providing file storage and file management interfaces).
3. **Peer-to-Peer (P2P) Computing**:
   Network model where all nodes are equal peers acting simultaneously as clients and servers. There is no central server bottleneck; peers join the network and locate resources through central registries or broadcast discovery protocols (e.g., BitTorrent).
4. **Web-Based / Cloud Computing**:
   Delivers virtualized computing resources, storage, and application software on demand over the Internet. It operates under three service models: IaaS (raw infrastructure/VMs), PaaS (managed development platforms), and SaaS (ready-to-use software like Gmail).
5. **Distributed Computing**:
   A network of physically separate, independent computer systems connected via LAN/WAN that share resources and coordinate tasks. The underlying operating system coordinates communications so users can access remote files and computing power seamlessly.

---

## Q.2 c) What are system calls? List and explain the different types of system calls. [10]

### Definition
A system call is the interface a process uses to request OS services.

### 6 Types of System Calls
1. **Process Control**:
   Handles process creation, execution, halting, and termination. It manages process priority, waits for specific time intervals or signals, and allocates or releases memory space for process execution.
   - *Example calls:* `fork()` (create new child process), `exit()` (terminate calling process), `wait()` (wait for child process state change), `brk()` / `sbrk()` (memory allocation).
2. **File Management**:
   Provides operations to create, delete, open, close, read, write, and reposition pointers within files stored on secondary storage. It also sets and reads file access attributes and directory permissions.
   - *Example calls:* `open()` (open file), `read()` (read data), `write()` (write data), `close()` (close file descriptor), `unlink()` (delete file link/file).
3. **Device Management**:
   Requests exclusive access to, releases, and operates physical or virtual hardware devices (e.g., disk drives, network cards, printers). Allows reading, writing, and configuring hardware device properties.
   - *Example calls:* `ioctl()` (device control operations), `read()`, `write()`, `request()` / `release()`.
4. **Information Maintenance**:
   Transfers operational metadata between user applications and the OS kernel. Allows programs to query or update system time, date, process identification numbers, memory usage, and OS version.
   - *Example calls:* `getpid()` (get current process ID), `time()` (get system time), `alarm()` (set process timer).
5. **Communications**:
   Manages the creation and deletion of inter-process communication (IPC) channels for exchanging messages or sharing memory between processes on the same host or across networks.
   - *Example calls:* `pipe()` (create unidirectional data channel), `shmget()` (allocate shared memory block), `send()` and `recv()` (socket message passing).
6. **Protection**:
   Manages security mechanisms and permissions controlling process access to files, memory, and system resources. Controls user privileges and file access modes to prevent unauthorized system access.
   - *Example calls:* `chmod()` (change file permission permissions), `umask()` (set file mode creation mask), `chown()` (change file ownership).
