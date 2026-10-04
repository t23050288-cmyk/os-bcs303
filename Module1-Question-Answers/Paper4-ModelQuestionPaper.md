# BCS303 — Model Question Paper-I (2023-24 CBCS Scheme)
## Module 1: Introduction to Operating Systems

---

## Q.01 a) Distinguish between the following terms: (i) Multiprogramming and Multitasking (ii) Multiprocessor System and Clustered System. [6]

### (i) Multiprogramming vs Multitasking

| Basis | Multiprogramming | Multitasking (Time Sharing) |
|---|---|---|
| Goal | Maximize CPU utilization | Fast interactive response |
| Switching | Only when a job waits | Very frequent |
| User interaction | Not required | Direct, interactive |

### (ii) Multiprocessor System vs Clustered System

| Basis | Multiprocessor System | Clustered System |
|---|---|---|
| Coupling | Tightly coupled — share bus, memory, clock | Loosely coupled — separate nodes, each with own memory |
| Connection | Internal (same machine) | Networked (LAN or fast interconnect) |
| Main purpose | Increased throughput | High availability / high-performance computing |

---

## Q.01 b) Define operating Systems. Explain the dual-mode operating system with a neat diagram. [7]

### Definition
An OS is system software that acts as an intermediary between a computer user and
the computer hardware, managing hardware and letting users run programs
conveniently.

### Dual-Mode Operation
**Points:**
1. Mode bit: kernel = 0, user = 1.
2. At boot, hardware starts in kernel mode; OS then runs user apps in user mode.
3. Trap/interrupt/system call switches mode to kernel (0); privileged
   instructions only run in kernel mode.

### Diagram
```
 user process:  [user process executing] -> calls system call -> [return from system call]
                        (mode bit = 1 = USER MODE)
                              |  trap, mode bit -> 0        ^ return, mode bit -> 1
                              v                              |
 kernel:                [execute system call] ----------------
                        (mode bit = 0 = KERNEL MODE)
```

---

## Q.01 c) With a neat diagram, explain the concept of the virtual machine. [7]

### Definition
A virtual machine abstracts hardware into several isolated execution
environments, each appearing as its own private computer.

### Diagram
```
(a) Non-virtual machine:          (b) Virtual machine:
      processes                    processes   processes   processes
         |                            |            |            |
   programming interface            kernel       kernel       kernel
         |                            VM1          VM2          VM3
       kernel                    ------------------------------------
         |                          virtual-machine implementation
      hardware                  ------------------------------------
                                             hardware
```

---

## Q.02 a) Explain the layered approach of operating system structure with a supporting diagram. [6]

### Definition
The OS is broken into layers, each resting on the layer below and using only
services from lower layers. Layer 0 = hardware; topmost layer = user interface.

### Points
1. Advantage: simplicity of construction/debugging — layers built & debugged
   bottom-up.
2. Disadvantage: less efficient — any call reaching hardware must pass through
   every intermediate layer.

### Diagram
```
layer N  — user interface
  :
layer 1
layer 0  — hardware
```

---

## Q.02 b) What are system calls? Briefly point out its types with illustrations. [6]

### Definition
A system call is the interface through which a user program requests OS services.

### 6 Types (with example)
1. **Process Control** — e.g. `fork()` creates a new process.
2. **File Management** — e.g. `open()` opens a file.
3. **Device Management** — e.g. `ioctl()` configures a device.
4. **Information Maintenance** — e.g. `getpid()` returns the process ID.
5. **Communications** — e.g. `pipe()` creates an IPC channel.
6. **Protection** — e.g. `chmod()` changes file permissions.

---

## Q.02 c) Explain the services of the operating system that are helpful for the user and the system. [8]

### Services for the user
1. User Interface, Program Execution, I/O Operations, File-System Manipulation,
   Communications, Error Detection.

### Services for the system (efficient operation)
2. Resource Allocation, Accounting, Protection and Security.
