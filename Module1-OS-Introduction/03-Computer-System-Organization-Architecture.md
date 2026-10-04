# 3. Computer System Organization & Architecture

Covers: "With a neat diagram, explain abstract view of the components of a
computer system", "What is caching? List and explain performance of various
levels of storage", interrupts, I/O structure, single/multi-processor systems,
clustered systems.

---

## 3.1 Computer System Organization

**Definition:** A general-purpose computer system consists of one or more CPUs and
several device controllers, all connected through a common **system bus** that
provides access to shared memory.

**Points:**
1. Each **device controller** manages a specific type of device (disk, USB,
   graphics) and has local buffer storage + special-purpose registers.
2. The OS has a **device driver** for each device controller, giving the rest of
   the OS a uniform interface to that device.
3. A **memory controller** synchronizes access to shared memory, since CPU and
   device controllers execute in parallel, competing for memory cycles.

### Diagram
```
   mouse  keyboard  printer   monitor
      \      |        |         |
       \     |        |         |
   disks  [USB controller]  [graphics adapter]
     \         |                  |
  [disk      system bus ----------┘
 controller]      |
      \           |
      [CPU] --- [memory]
```

---

## 3.2 Interrupts

**Definition:** An interrupt is a signal sent to the CPU (usually via the system
bus) that alerts it to an event needing attention — the CPU stops what it's
doing and transfers control to a fixed location (the interrupt handler).

**Points:**
1. Interrupts can be **hardware-generated** (device signals the CPU) or
   **software-generated** — a **trap** or **exception** (caused by an error like
   division by zero, or a deliberate system call request).
2. The CPU has an **interrupt-request line** it senses after every instruction.
3. The **interrupt vector** is a table of pointers (stored in low memory) to
   interrupt service routines, indexed by a unique interrupt number — this avoids
   a slow linear search through all possible handlers.
4. After servicing, the interrupt handler restores the saved state and resumes
   the interrupted computation exactly where it left off.
5. Most CPUs have 2 interrupt lines: **nonmaskable** (for critical errors like
   unrecoverable memory faults — can't be turned off) and **maskable** (used by
   device controllers; can be temporarily disabled during critical sections).
6. **Interrupt chaining**: each interrupt-vector slot points to a *list* of
   handlers (not just one), since there are usually more devices than vector slots.
7. **Interrupt priority levels** let the CPU defer low-priority interrupts and let
   high-priority ones preempt them.

### Interrupt-Driven I/O Cycle
```
1. Device driver initiates I/O         ---> 2. I/O controller initiates I/O
7. CPU resumes interrupted task <---         3. input ready/output done/error
         ^                                      generates interrupt signal
5. interrupt handler processes data,  <--- 4. interrupt signal
   returns from interrupt
         |
6. (returns to step 7)
```

---

## 3.3 Storage Structure & the Memory Hierarchy

**Definition:** Programs must be loaded into **main memory (RAM)** to run — the
CPU can only directly load instructions/data from memory, not from disk.

**Points:**
1. Main memory is commonly **DRAM** (dynamic RAM); it is **volatile** — loses
   content when power is lost.
2. Programs/data can't live in RAM permanently because: (a) RAM is usually too
   small, and (b) RAM is volatile.
3. **Secondary storage** (HDDs, SSDs/NVM) extends main memory — holds data
   permanently, but is much slower.
4. **Tertiary storage** (magnetic tape, optical disks) — used for backups/archival,
   slow and large, not performance-critical.
5. **Caching**: data is normally kept in a storage system; as it's used, it's
   copied into a faster, temporary **cache**. Next time that data is needed, we
   check the cache first — if present ("hit"), use it directly; if not ("miss"),
   fetch from the source and cache a copy for next time.
6. Because caches are limited in size, **cache replacement policy** matters a lot
   for performance.
7. **Cache coherency**: in a multiprocessor system, each CPU has its own local
   cache — if a value is updated in one cache, all other caches holding a copy
   must be updated too (usually handled by hardware, below the OS level).

### Storage Hierarchy (fastest/smallest at top, slowest/largest at bottom)
```
        registers        <- fastest, smallest, volatile
          cache
       main memory
   ─────────────────────  (dashed line: volatile above, nonvolatile below)
   nonvolatile memory (SSD/NVM)
      hard-disk drives
        optical disk
       magnetic tapes      <- slowest, largest, nonvolatile
```

**Points on hierarchy:**
- As you move down: capacity increases, speed decreases, cost per byte decreases.
- Volatile storage (registers, cache, main memory) loses data on power loss.
- Nonvolatile storage (NVM, HDD, tape) retains data without power.

---

## 3.4 I/O Structure & DMA

**Definition:** A large part of OS code manages I/O devices and data movement
between them and memory.

**Points:**
1. Plain interrupt-driven I/O works fine for small data transfers but creates
   high overhead for bulk transfers (one interrupt per byte would be too slow).
2. **Direct Memory Access (DMA)** solves this: after the device driver sets up
   buffers/pointers/counters, the device controller transfers an **entire block**
   of data directly to/from memory **without CPU intervention**.
3. Only **one interrupt per block** is generated (not one per byte) — the CPU is
   free to do other work while the transfer happens.

---

## 3.5 Computer System Architecture

### Single-Processor Systems
**Definition:** A system with one general-purpose CPU (with a single core)
capable of running a general-purpose instruction set.

**Points:**
1. May still contain special-purpose processors (disk controller, keyboard
   microcontroller) — these run a limited instruction set and don't run user
   processes; using them does **not** make it a multiprocessor system.
2. Very few modern systems are truly single-processor by this strict definition.

### Multiprocessor Systems
**Definition:** Systems with two or more CPUs in close communication, sharing the
bus, memory, and peripherals. Also called parallel or tightly-coupled systems.

**3 Advantages:**
1. **Increased throughput** — more work done, though speed-up with N processors
   is **less than N** due to overhead/contention for shared resources.
2. **Economy of scale** — multiprocessor systems cost less than N equivalent
   single-processor systems since they share peripherals, storage, power supply.
3. **Increased reliability** — if one processor fails, the system doesn't halt,
   just slows down (**graceful degradation**); some systems are **fault
   tolerant** — they detect, diagnose, and correct the failure.

**Types:**
1. **Asymmetric multiprocessing** — a master processor controls/schedules work
   for slave processors.
2. **Symmetric multiprocessing (SMP)** — all processors are peers; no
   master-slave relationship; each has its own registers/cache, but memory is
   shared. Most modern OSes (Windows, Linux, macOS) support SMP.
3. **NUMA (Non-Uniform Memory Access)** — each CPU/group has its own local memory
   (fast, no contention) plus a shared interconnect to access others' memory
   (slower). Scales better than plain SMP as more processors are added.
4. **Multicore** — multiple computing cores on a single chip; faster
   on-chip communication, lower power than multiple single-core chips.

### Clustered Systems
**Definition:** Two or more individual systems ("nodes") joined together, sharing
storage and connected via a LAN or faster interconnect — "loosely coupled."

**Points:**
1. Mainly used for **high availability** — service continues even if one or more
   nodes fail (redundancy).
2. **Asymmetric clustering** — one machine is in **hot-standby mode**, only
   monitoring; takes over only if the active server fails.
3. **Symmetric clustering** — two or more nodes run applications AND monitor each
   other — more efficient (uses all hardware) but needs multiple apps available.
4. Also used for **high-performance computing** via **parallelization** —
   splitting a program into parts that run concurrently across cluster nodes,
   then combining results.
