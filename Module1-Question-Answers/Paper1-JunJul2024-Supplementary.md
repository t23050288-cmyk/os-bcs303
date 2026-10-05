# BCS303 — June/July 2024 Supplementary Exam
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Define system call. List the types of system calls. [6]

### Definition
A system call is the programming interface through which a user program requests
a service from the operating system.

### Points
1. Usually written in C/C++; invoked as a **trap** into kernel mode.
2. Most programmers use an **API** (e.g. POSIX, Windows API) rather than raw
   system calls — this gives greater program portability.
3. Each system call has a unique number, looked up via a **system call table**.

### 6 Types of System Calls
1. **Process Control**:
   Controls process execution, creation, and termination. It manages process attributes, waits for time or events, and allocates or frees memory space.
   - *Example calls:* `fork()` (create process), `exit()` (terminate), `wait()` (wait for event), `allocate()` (memory).
2. **File Management**:
   Handles file operations such as creating, deleting, opening, closing, reading, writing, and repositioning pointers in files. It also manages file attributes like permissions.
   - *Example calls:* `open()`, `read()`, `write()`, `close()`, `unlink()` (delete file).
3. **Device Management**:
   Requests, releases, and operates hardware devices like disk drives and printers. It allows programs to read from, write to, and set properties of physical or virtual devices.
   - *Example calls:* `ioctl()` (device control), `read()`, `write()`, `request()`.
4. **Information Maintenance**:
   Transfers status data between user programs and the operating system. It allows programs to read or set system date, time, process IDs, and performance statistics.
   - *Example calls:* `getpid()` (get process ID), `time()`, `alarm()`.
5. **Communications**:
   Manages data transfer and message exchanges between different processes on the same system or across a network. Supports message passing and shared memory models.
   - *Example calls:* `pipe()` (IPC channel), `shmget()` (shared memory), `send()`, `recv()`.
6. **Protection**:
   Controls access to computer resources, files, and processes to prevent illegal access. Sets file permissions and grants or revokes user rights.
   - *Example calls:* `chmod()` (change permissions), `umask()`, `chown()` (change owner).

---

## Q.1 b) With a neat figure, explain the concept of virtual machines. [6]

### Definition
Virtualization abstracts a single computer's hardware into several different
execution environments, each appearing to run on its own private computer.

### Points
1. Each environment can run a different OS (e.g. Windows + Linux) simultaneously.
2. **Host OS** runs on the real hardware; **Guest OS** runs inside a VM.
3. First appeared as IBM's VM Operating System in 1972.
4. The VMM (virtual machine manager) runs in kernel mode; each VM it manages runs
   only in user mode.

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

## Q.1 c) Define Operating System. Explain multiprogramming and time sharing operating system. [8]

### Definition
An operating system is system software that acts as an intermediary between a
computer user and the computer hardware, managing hardware and letting users run
programs conveniently and efficiently.

### Multiprogramming
**Points:**
1. Keeps several jobs in memory at once so the CPU always has something to
   execute — increases CPU utilization.
2. When the running job needs to wait (e.g. I/O), the OS switches to another job
   instead of leaving the CPU idle.
3. As long as one job is ready, the CPU is never idle.

### Time-Sharing (Multitasking)
**Points:**
1. Logical extension of multiprogramming — CPU switches among processes so
   **frequently** that users get fast interactive response.
2. Requires an interactive system; response time should be under 1 second.
3. Each user feels like they have the whole system, even though it's shared.
4. Needs memory management, CPU scheduling, and often virtual memory.

### Diagram (multiprogramming memory layout)
```
0 ┌────────────────────┐
  │   operating system  │
  ├────────────────────┤
  │  job 1 │ job 2 │ job 3 │ job 4  │
512M└────────────────────┘
```

---

## Q.2 a) List the responsibilities of the operating system for process management and memory management. [6]

### Process Management Responsibilities
1. Creating and deleting both user and system processes.
2. Scheduling processes/threads on the CPU.
3. Suspending and resuming processes.
4. Providing mechanisms for process synchronization.
5. Providing mechanisms for process communication (IPC).

### Memory Management Responsibilities
1. Keeping track of which parts of memory are used, and by which process.
2. Allocating and deallocating memory space as needed.
3. Deciding which processes/data to move into and out of memory.

---

## Q.2 b) Different between kernel mode and user mode operation of operating systems. [6]

### Definition
Dual-mode operation uses a hardware **mode bit** to distinguish between tasks
executed on behalf of the OS (kernel mode) and tasks executed on behalf of a user
program (user mode).

### Comparison Table

| Basis | User Mode | Kernel Mode |
|---|---|---|
| Mode bit | 1 | 0 |
| Who runs | User application code | OS code |
| Privileged instructions | Cannot execute (traps as illegal) | Can execute |
| Hardware/I/O access | Indirect only, via system calls | Direct |
| Switch trigger | — | Trap, interrupt, or system call |

### Points
1. At boot, hardware starts in kernel mode; OS loads and starts user apps in
   user mode.
2. Any trap/interrupt automatically switches the mode bit to kernel mode (0).
3. Privileged instructions (I/O control, timer management) only run in kernel
   mode — attempting them in user mode traps to the OS as an illegal instruction.

---

## Q.2 c) Discuss the services that are provided by the operating systems for users and its efficient operation. [8]

### Services helpful to the user
1. **User Interface** — CLI, GUI, or batch.
2. **Program Execution** — load, run, terminate programs.
3. **I/O Operations** — transfer data to/from devices via drivers.
4. **File-System Manipulation** — create/delete/search files & directories.
5. **Communications** — IPC between processes.
6. **Error Detection** — hardware, I/O, and program error handling.

### Services for efficient system operation
7. **Resource Allocation** — CPU, memory, storage, I/O devices shared among users.
8. **Accounting** — track resource usage for billing/statistics.
9. **Protection and Security** — control access to resources; defend against
   external/internal attacks.
