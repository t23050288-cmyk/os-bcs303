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

### Points
1. Traditional/time-sharing computing.
2. Client-Server computing (compute-server, file-server).
3. Peer-to-Peer computing.
4. Web-based/Cloud computing.
5. Distributed computing.

---

## Q.2 c) What are systems calls? List and explain the different types of systems calls. [8]

### Definition
A system call is the interface a process uses to request a service from the OS.

### 6 Types
1. Process Control
2. File Management
3. Device Management
4. Information Maintenance
5. Communications
6. Protection
