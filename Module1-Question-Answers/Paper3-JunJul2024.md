# BCS303 — June/July 2024 Exam
## Module 1: Introduction to Operating Systems

---

## Q.1 a) Explain multi programming and time sharing systems. [7]

### Multiprogramming
**Definition:** Keeps several jobs in memory simultaneously so the CPU always has
something to execute, maximizing CPU utilization.

**Points:**
1. When a job needs to wait (e.g. I/O), the OS switches to another ready job.
2. As long as at least one job is ready, the CPU is never idle.
3. Doesn't inherently provide user interaction.

### Time Sharing
**Definition:** A logical extension of multiprogramming — CPU switches among
processes so frequently that users get fast interactive response.

**Points:**
1. Requires an interactive (hands-on) system.
2. Response time should typically be under 1 second.
3. Needs memory management, CPU scheduling, and often virtual memory.

---

## Q.1 b) Explain the dual mode operation in operating systems with a neat block diagram. [7]

### Definition
Dual-mode operation uses a hardware **mode bit** to distinguish OS code execution
(kernel mode, bit=0) from user program execution (user mode, bit=1), protecting
the OS and other users from a misbehaving program.

### Points
1. At boot, hardware starts in kernel mode; OS then starts user apps in user mode.
2. A trap/interrupt/system call switches mode bit to kernel mode (0).
3. **Privileged instructions** (I/O control, timer, mode switching) only execute
   in kernel mode — attempting them in user mode traps as illegal.

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

## Q.1 c) What are virtual machines? Explain with a neat figure. [6]

### Definition
A virtual machine abstracts a computer's hardware into several isolated execution
environments, each appearing to run on its own private computer.

### Points
1. Host OS runs on real hardware; Guest OS runs inside a VM, managed by a VMM.
2. VMM runs in kernel mode; VMs run only in user mode.
3. Benefits: isolation (a crash in one VM doesn't affect others), easier system
   development/testing, system consolidation.

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

## Q.2 a) What are system calls? Briefly explain different types of system calls. [7]

### Definition
A system call is the interface through which a user program requests a service
from the OS kernel.

### 6 Types
1. **Process Control** — create/terminate process, allocate/free memory.
2. **File Management** — create, open, read, write, close files.
3. **Device Management** — request/release device, read/write.
4. **Information Maintenance** — get/set time, system data.
5. **Communications** — send/receive messages, create connections.
6. **Protection** — control resource access permissions.

---

## Q.2 b) List and explain the services provided by OS for the user in efficient operation of a system. [7]

### Services for the user
1. User Interface, Program Execution, I/O Operations, File-System Manipulation,
   Communications, Error Detection.

### Services for efficient operation
2. Resource Allocation, Accounting, Protection and Security.

---

## Q.2 c) What are micro kernels? With a neat figure, explain the micro kernel structure? Point out their advantages over layered approach. [6]

### Definition
A microkernel removes all non-essential components from the kernel,
implementing them as user-space system/application programs — keeping the kernel
itself as small as possible.

### Points
1. Microkernel's main job: provide communication (message passing) between
   client programs and the various services running in user space.
2. Typically provides only basic process/memory management + IPC.

### Diagram
```
 user mode:    [Application Program] [File System] [Device Driver]
                        ^  messages  ^  messages  ^
 kernel mode:  --------[ Interprocess Communication | memory mgmt | CPU scheduling ]
                                   microkernel
                                      |
                                  hardware
```

### Advantages over Layered Approach
1. **Easier expansion** — add a new system application without rebuilding the
   kernel, unlike layered systems where every layer boundary matters.
2. **More direct communication** — services talk to clients via message passing
   without passing through multiple intermediary layers down to hardware.
3. **Smaller, more secure kernel** — fewer kernel bugs since most code runs in
   user space, isolated by the hardware's dual-mode protection.

(Disadvantage: message-passing between user space and kernel space costs more
than the direct function calls used within a layered or monolithic kernel.)
