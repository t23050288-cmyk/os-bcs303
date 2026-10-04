# BCS303 — June/July 2025 Makeup Exam
## Module 1: Introduction to Operating Systems

---

## Q.1 a) With neat diagram, Explain abstract view of the components of a computer system. [6]

### Definition
A computer system has 4 components: Hardware, Operating System, Application
Programs, and Users.

### Diagram
```
            user 1    user 2    user 3   ...   user n
              |         |         |              |
          compiler  assembler  text editor ... database system
              |_________|_________|______________|
                   system and application programs
                              |
                        operating system
                              |
                        computer hardware
                     (CPU, memory, I/O devices)
```

### Points
1. Hardware provides basic computing resources.
2. Application programs define how resources solve user problems.
3. The OS controls hardware and coordinates its use among applications/users.

---

## Q.1 b) With neat diagram, explain virtual, non virtual and VM ware architecture. [8]

### Non-Virtual vs Virtual
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

### VMware Architecture
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
1. In a non-virtual system, processes talk directly to one kernel on bare
   hardware.
2. In a virtual system, each guest OS believes it has its own hardware, but
   really runs atop a virtualization layer managed by the VMM/host.
3. VMware's virtualization layer abstracts physical hardware into isolated VMs,
   each with its own virtual CPU/memory/devices.

---

## Q.1 c) Explain with neat diagram Dual-Mode operation. [6]

### Points
1. Mode bit: kernel=0, user=1.
2. Trap/interrupt/system call switches to kernel mode.
3. Privileged instructions only run in kernel mode.

### Diagram
```
 user mode (bit=1): user process executing -> system call -> return from system call
                              |  trap                          ^ return
                              v                                |
 kernel mode (bit=0):              execute system call ---------
```

---

## Q.2 a) Explain types of system calls provided by operating system. [6]

### 6 Types
1. Process Control
2. File Management
3. Device Management
4. Information Maintenance
5. Communications
6. Protection

---

## Q.2 b) Explain with neat diagram simple structure of MS-DOS layer structure and unix system structure. [8]

### MS-DOS Layer Structure
```
          application program
                 |
         resident system program
                 |
          MS-DOS device drivers
                 |
           ROM BIOS device drivers
```

### UNIX System Structure
```
          application programs
                 |
            system programs
   ------------------------------------
                  kernel
   (file system | CPU scheduling | memory management | device drivers)
   ------------------------------------
                 hardware
```

### Points
1. **MS-DOS**: no clear separation — applications can access I/O routines
   directly, so a single app bug can crash the whole system.
2. **UNIX**: split into kernel (via system calls) and system programs — much
   more robust separation than MS-DOS.

---

## Q.2 c) Explain operating-system services. [6]

### Services for the user
User Interface, Program Execution, I/O Operations, File-System Manipulation,
Communications, Error Detection.

### Services for efficient operation
Resource Allocation, Accounting, Protection and Security.
