# 7. OS Design & Implementation, and OS Structure

Covers: "Explain the layered approach of operating system structure", "What are
micro kernels? ... Point out their advantages over layered approach", "Explain
with neat diagram simple structure of MS-DOS layer structure and unix system
structure", "Explain the different architecture of OS starting from Simple
Structure, Layered Structure, Micro Kernels, Modules and Hybrid Systems", "Discuss
in detail about Operating System structure".

---

## 7.1 Design Goals

**Definition:** Before building an OS, its goals and specifications must be
defined — split into **user requirements** and **system requirements**.

**Points:**
1. Highest-level design is shaped by the hardware chosen and system type: batch,
   time-shared, single-user, multiuser, distributed, real-time, or general purpose.
2. **User requirements** — features users care about: convenient to use, easy to
   learn, reliable, safe, fast.
3. **System requirements** — written for the developers who build/maintain the
   OS: easy to design/implement/maintain, flexible, reliable, error-free,
   efficient.

---

## 7.2 Mechanisms vs. Policies

**Definition:** **Mechanisms** determine **how** something is done; **policies**
determine **what** is to be done.

**Points:**
1. Example: a timer's hardware countdown is the *mechanism*; deciding *how long*
   to set the timer for is the *policy*.
2. Policies change more often than mechanisms over a system's life.
3. If mechanism and policy are kept properly separated, a policy change (e.g.
   adjusting a scheduling priority rule) doesn't require rewriting the underlying
   mechanism — just adjusting parameters or config.

---

## 7.3 Implementation

**Points:**
1. Traditionally OSes were written in assembly language. Modern OSes are mostly
   written in **C or C++**, with only critical/performance-sensitive sections in
   assembly.
2. The first OS not written fully in assembly was the **Master Control Program
   (MCP)**.
3. **Advantages of a higher-level language:** code is written faster, more
   compact, easier to port to other hardware, easier to understand/debug.
4. **Disadvantages:** potentially reduced speed and increased memory/storage
   requirements compared to hand-tuned assembly.

---

## 7.4 Operating System Structures

### 1. Simple Structure
**Definition:** No well-defined internal structure — the system grew
organically beyond its original small/simple scope. Example: **MS-DOS**.

**Points:**
1. In MS-DOS, interfaces and functionality levels aren't well separated —
   application programs can access basic I/O routines directly, writing straight
   to the display/disk.
2. This freedom is dangerous: a bug in **any** application can crash the entire
   system, since there's no dual-mode-style isolation.
3. **UNIX**, in contrast, is split into two separable parts: the **kernel**
   (providing file system, CPU scheduling, memory management via system calls)
   and **system programs** (layered above the kernel).

### Diagram (MS-DOS layer structure)
```
          application program
                 |
         resident system program
                 |
          MS-DOS device drivers
                 |
           ROM BIOS device drivers
```

### 2. Layered Approach
**Definition:** The OS is broken into a number of layers (levels), each resting on
the layer below and using only the services of layers below it. Layer 0 =
hardware; the topmost layer = user interface.

**Points:**
1. Each layer is implemented using only operations/data of lower layers.
2. **Advantage — simplicity of construction & debugging**: layers are built and
   debugged bottom-up; if layer N misbehaves, the bug must be in layer N itself
   (lower layers are already verified).
3. A layer **hides** its implementation details from the layers above it.
4. **Disadvantages:**
   - Each layer must be carefully, appropriately defined (hard to partition
     cleanly).
   - **Less efficient** — any interaction eventually reaching layer 0 (hardware)
     must pass through every intermediate layer, adding overhead.

### Diagram (layered OS)
```
layer N  — user interface
  :
layer 1
layer 0  — hardware
```

### 3. Microkernels
**Definition:** Removes all **non-essential** components from the kernel,
implementing them instead as **system/user-level programs**, keeping the kernel
itself as small as possible.

**Points:**
1. The microkernel's main job: provide **communication (message passing)**
   between client programs and the various services (which run in user space).
2. Typically provides only basic process & memory management + IPC.
3. **Benefit:** easier system expansion — just add more user-space system
   applications, no need to rebuild/modify the kernel.
4. **Advantage over layered approach:** more modular — a service doesn't have to
   go through every intermediate layer; direct message-based communication.
5. **Disadvantage:** **performance overhead** from user-space ↔ kernel-space
   message passing (context switches cost more than a simple function call).
6. **Mach** was the first/best-known microkernel — now a core component of
   macOS/Mac OS X.

### Diagram (microkernel)
```
 user mode:    [Application Program] [File System] [Device Driver]
                        ^  messages  ^  messages  ^
 kernel mode:  --------[ Interprocess Communication | memory mgmt | CPU scheduling ]
                                   microkernel
                                      |
                                  hardware
```

### 4. Modules
**Definition:** A relatively small core kernel, plus a set of **modules** that
can be dynamically linked in — the modern, object-oriented approach.
Examples: **Solaris, Linux, macOS**.

**Points:**
1. Like layers, each module has clearly defined tasks/interfaces — but **unlike**
   layers, any module is free to call **any other module directly** (no need to
   pass through intermediaries).
2. Like microkernels, the core kernel is small — but **unlike** microkernels, it
   doesn't need message passing, since modules talk to each other directly.
3. This gives the **flexibility of layers + the efficiency of direct calls**
   without microkernel-style message-passing overhead.

### 5. Hybrid Systems
**Definition:** Most modern OSes (Linux, Windows, macOS) are **hybrid** — they
combine ideas from multiple structures (e.g. a monolithic-ish kernel with
modules, plus some microkernel-style services) rather than following one pure
model.

---

## 7.5 Virtual Machines (brief — see file 08 for full detail)

A **virtual machine** abstracts hardware into multiple isolated execution
environments, each appearing to run on its own private computer — essentially a
different way of structuring/virtualizing the system beneath multiple guest OSes.
