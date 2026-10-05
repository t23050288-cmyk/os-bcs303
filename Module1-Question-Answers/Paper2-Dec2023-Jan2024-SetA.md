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

### OS Structures
1. **Simple Structure**:
   In a simple structure, there is no clear boundary or separation between layers (e.g., MS-DOS). Application programs can directly access low-level BIOS I/O routines and hardware. If an application contains a bug, it can crash the entire system because there is no hardware-enforced mode protection.
2. **Layered Approach**:
   The OS is divided into distinct layers (Layer 0 = hardware, top layer = user interface). Each layer is built on top of lower layers and uses only the services provided by the layer directly below it. This makes system design and debugging easy, but it decreases efficiency because requests must pass through every intermediate layer down to hardware.
3. **Microkernels**:
   A microkernel removes all non-essential components from the kernel and implements them as user-space system programs. The microkernel itself stays minimal, handling process/memory management and inter-process communication (IPC) via message passing (e.g., Mach). It is easy to extend and secure, but message-passing context switches introduce performance overhead.
4. **Modules (Loadable Kernel Modules)**:
   The modern object-oriented approach where the OS consists of a small core kernel that dynamically loads feature modules into kernel memory at boot or runtime (e.g., Linux, Solaris). Modules are like layers because each has a clean interface, but any module can call any other module directly without layer passing or microkernel message-passing overhead.

### OS Operations
1. **Interrupt-Driven Architecture**:
   Modern operating systems are interrupt-driven; if there are no user tasks or hardware events, the system sits idle waiting for something to happen. Hardware events send interrupts, while software errors or system call requests generate software traps to trigger OS handler routines.
2. **Dual-Mode Operation**:
   Uses a hardware mode bit (0 = kernel mode, 1 = user mode) to protect the OS from errant or malicious user programs. Privileged instructions (such as direct I/O manipulation) can only execute in kernel mode; any attempt to run them in user mode causes a hardware trap to the OS.
3. **Hardware Timer**:
   A hardware timer interrupts the CPU after a specified time period to guarantee that the OS regularly regains control of the processor. This prevents a user program from getting caught in an infinite loop or hogging the system indefinitely.

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

### 6 Types of System Calls
1. **Process Control**:
   Manages process execution, creation, and termination. Controls process attributes, process synchronization, event waiting, and memory allocation or deallocation.
   - *Example calls:* `fork()` (create process), `exit()` (terminate process), `wait()` (wait for child process), `allocate()`.
2. **File Management**:
   Handles file operations including creating, deleting, opening, closing, reading, writing, and repositioning file pointers. Also reads and updates file permissions and attributes.
   - *Example calls:* `open()`, `read()`, `write()`, `close()`, `unlink()` (delete file).
3. **Device Management**:
   Requests, releases, and manages hardware devices such as disk drives, terminals, and printers. Reads from, writes to, and configures device attributes.
   - *Example calls:* `ioctl()` (device control), `read()`, `write()`, `request()`.
4. **Information Maintenance**:
   Transfers system and process metadata between user applications and the OS kernel. Gets or sets current time, date, process IDs, and system environment statistics.
   - *Example calls:* `getpid()` (get process ID), `time()`, `alarm()`.
5. **Communications**:
   Manages message passing and connection establishment between processes running locally or across a network. Supports both message-passing and shared-memory communication models.
   - *Example calls:* `pipe()` (inter-process communication channel), `shmget()` (shared memory allocation), `send()`, `recv()`.
6. **Protection**:
   Controls and restricts process access to system resources, memory, and files according to safety rules. Sets user permissions and access control lists.
   - *Example calls:* `chmod()` (change access mode), `umask()`, `chown()` (change file owner).

---

## Q.2 c) What are various system programs? Explain. [5]

### Definition
System programs provide a convenient environment for program development and
execution, sitting between the user and raw system calls.

### 6 Categories of System Programs
1. **File Management**:
   Programs used to create, delete, copy, rename, print, dump, list, and manipulate files and directories stored on disk.
   - *Examples:* `ls` (list files), `cp` (copy file), `rm` (remove file), `mkdir` (create directory).
2. **Status Information**:
   Utilities that retrieve and display system status details such as system date, time, available memory, disk space, logged-in users, and performance metrics.
   - *Examples:* `date`, `top` (process/memory usage), `df` (disk free space), `who`.
3. **File Modification**:
   Text editors and editing utilities that allow users to view, search, and edit the contents of files stored on disk.
   - *Examples:* `nano`, `vim`, `gedit`, `grep`.
4. **Programming-Language Support**:
   Development tools provided with the OS, including compilers, assemblers, debuggers, and language interpreters for code translation and execution.
   - *Examples:* `gcc` (C compiler), `gdb` (debugger), `python`, `javac`.
5. **Program Loading and Execution**:
   System tools that assemble object files, link libraries, load executable binaries into main memory, and prepare them for CPU execution.
   - *Examples:* `ld` (linker/loader), system loaders, interactive runtime debuggers.
6. **Communications**:
   Utilities that create virtual connections between machines, allow users to transfer files, send electronic messages, and browse web pages across networks.
   - *Examples:* `ssh` (remote login), `ftp`/`sftp` (file transfer), `mail`, `ping`, `curl`.
