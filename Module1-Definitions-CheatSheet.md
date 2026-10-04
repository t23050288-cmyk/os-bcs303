# Module 1 — All Definitions Cheat Sheet (Easy to Understand & Tell to Ma'am/Sir)

> Each concept: **simple definition → key points → diagram where useful**
> Read this once before the exam and you can explain any term confidently.

---

## 1. Operating System

**What it is:** System software that acts as an intermediary between a computer
user and the computer hardware — manages hardware and lets users run programs
conveniently and efficiently.

**Points:**
- 4 components of a computer system: Hardware, OS, Application programs, Users.
- **Analogy:** like a government — does no useful work itself, just provides an
  environment where other programs can do useful work.
- Goals: easy to use, efficient hardware use, resource allocator.

---

## 2. User View vs System View

**User view:** depends on who's using it — standalone PC (ease of use), shared
terminal (maximize utilization), workstation (ease of use + resource sharing),
embedded (no interaction), handheld (battery-efficient).

**System view:** the OS is a **resource allocator** (assigns CPU/memory/storage
fairly) and a **control program** (prevents errors/improper hardware use).

---

## 3. Multiprogramming

**What it is:** Keeping several jobs in memory at once so the CPU always has
something to run — never sits idle waiting for one job's I/O.

**Points:**
- When a job waits (e.g. for I/O), OS switches to another ready job.
- Doesn't require user interaction.

---

## 4. Multitasking (Time Sharing)

**What it is:** A logical extension of multiprogramming — CPU switches among
processes so **frequently** that each user feels they have a dedicated machine.

**Points:**
- Needs interactive I/O; response time should be under 1 second.
- Needs memory management, CPU scheduling, often virtual memory.

---

## 5. Dual-Mode Operation

**What it is:** A hardware mode bit (kernel=0, user=1) that separates OS
execution from user program execution, protecting the OS from errant programs.

**Points:**
- Trap/interrupt/system call switches to kernel mode.
- Privileged instructions (I/O control, timer, mode switch) only run in kernel
  mode — attempting them in user mode traps as illegal.
- At boot: hardware starts in kernel mode; OS then runs user apps in user mode.

**Diagram:**
```
user mode (1): user process -> system call -> return from system call
                     | trap                       ^ return
                     v                             |
kernel mode (0):          execute system call ------
```

---

## 6. Timer

**What it is:** Hardware that interrupts the CPU after a set period, ensuring
the OS always regains control (prevents infinite loops from freezing the system).

---

## 7. System Call

**What it is:** The programming interface a process uses to request a service
from the OS kernel (e.g. open a file, create a process).

**Points:**
- Invoked as a trap; switches mode bit to kernel mode.
- Most programmers use an **API** (POSIX, Windows API) instead of raw syscalls
  — gives program portability.
- 3 ways to pass parameters: in registers, via a memory block (address passed in
  a register), or pushed/popped on the stack.

**6 Types (easy to remember: Process, File, Device, Information, Communication,
Protection):**
1. Process Control — `fork()`, `exit()`
2. File Management — `open()`, `read()`, `write()`
3. Device Management — `ioctl()`
4. Information Maintenance — `getpid()`, `time()`
5. Communications — `pipe()`, `send()`
6. Protection — `chmod()`

---

## 8. Interrupt

**What it is:** A signal (hardware or software) that alerts the CPU to an event
needing attention — the CPU stops, services the event, then resumes.

**Points:**
- **Trap/exception** = software-generated interrupt (error, or a system call).
- **Interrupt vector** = table of pointers to handlers, indexed by interrupt
  number — avoids a slow search.
- **Maskable** interrupts can be temporarily disabled; **nonmaskable** cannot
  (reserved for critical errors).

---

## 9. Storage Hierarchy & Caching

**What it is:** Storage systems arranged from fastest/smallest/volatile at the
top to slowest/largest/nonvolatile at the bottom.

```
registers -> cache -> main memory -> NVM/SSD -> HDD -> optical disk -> tape
(fastest, smallest)                                      (slowest, largest)
```

**Caching:** copying frequently-used data into a faster temporary store. Check
cache first ("hit" = use directly; "miss" = fetch from source, then cache it).

---

## 10. DMA (Direct Memory Access)

**What it is:** A method for transferring an entire **block** of data between a
device and memory **without CPU intervention** — only one interrupt per block,
not one per byte. Used for bulk transfers (disk I/O).

---

## 11. Single-Processor vs Multiprocessor vs Clustered Systems

| Type | Description |
|---|---|
| Single-processor | One general-purpose CPU (special-purpose device processors don't count) |
| Multiprocessor (SMP) | 2+ CPUs, tightly coupled, share bus/memory; all CPUs are peers |
| NUMA | Each CPU has local memory (fast) + shared interconnect to others' memory (slower) |
| Clustered | 2+ independent nodes, loosely coupled, networked, share storage — for high availability |

**3 Multiprocessor Advantages:** increased throughput, economy of scale,
increased reliability (graceful degradation / fault tolerance).

---

## 12. Mechanisms vs Policies

**Mechanisms** = **how** something is done (e.g. the timer's countdown
hardware). **Policies** = **what** is to be done (e.g. how long to set the
timer for). Keeping them separate lets policy change without rewriting the
mechanism.

---

## 13. OS Structures

| Structure | Idea | Pro | Con |
|---|---|---|---|
| Simple (MS-DOS) | No layer separation | Simple | One bug crashes everything |
| Layered | Layers use only lower layers | Easy debug | Slower (every call passes through all layers) |
| Microkernel | Minimal kernel + user-space services via messages | Easy to extend, secure | Message-passing overhead |
| Modules | Small kernel + modules calling each other directly | Fast + flexible | — |
| Hybrid | Combines multiple structures | Used by Linux/Windows/macOS | — |

---

## 14. Virtual Machine

**What it is:** Abstracts a computer's hardware into several isolated execution
environments ("VMs"), each appearing to run on its own private computer.

**Points:**
- Host OS = runs on real hardware. Guest OS = runs inside a VM.
- VMM (hypervisor) runs in kernel mode; VMs run only in user mode.
- Benefits: isolation, easier dev/testing, system consolidation.
- First appeared: IBM's VM OS, 1972.

---

## 15. JVM (Java Virtual Machine)

**What it is:** A software layer that runs Java **bytecode** (compiled from
Java source), giving "compile once, run anywhere" portability.

**Points:** JVM = class loader + Java interpreter; also handles memory
management/garbage collection.

---

## 16. Protection vs Security

**Protection:** mechanisms controlling access of processes/users to system
resources (e.g. memory-addressing hardware, timers, device-control registers).

**Security:** defending the system from external/internal attacks (viruses,
denial-of-service, identity theft, theft of service).

---

## 17. Computing Environments

| Environment | Description |
|---|---|
| Traditional/Time-sharing | Batch or interactive, CPU time-sliced among users |
| Client-Server | Clients request, servers respond (compute-server / file-server) |
| Peer-to-Peer (P2P) | All nodes are peers — no fixed client/server role, no bottleneck |
| Web-based/Cloud | Resources delivered over the web — IaaS / PaaS / SaaS |
| Distributed | Physically separate systems networked to share resources |

---

## 18. Special-Purpose Systems

**Multimedia systems:** handle audio/video with **time-restricted delivery**
(e.g. 30 fps streaming).

**Handheld systems:** PDAs/smartphones — limited memory, slower (power-saving)
processors, small screens; succeed due to portability.

---

## Quick Memory Summary (one-liners)

| Term | One-line definition |
|---|---|
| Operating System | Intermediary between user and hardware; resource allocator + control program |
| Multiprogramming | Keep multiple jobs in memory so CPU is never idle |
| Multitasking | Fast CPU switching for interactive, simultaneous-feeling execution |
| Dual-mode operation | Mode bit separates kernel-mode OS code from user-mode programs |
| System call | Interface for a user program to request an OS service |
| Interrupt | Signal that alerts the CPU to an event needing attention |
| DMA | Block data transfer between device and memory, no CPU involvement |
| Multiprocessor (SMP) | 2+ peer CPUs sharing memory/bus for more throughput |
| Clustered system | 2+ networked nodes sharing storage for high availability |
| Virtual Machine | Isolated execution environment that mimics its own private computer |
| Microkernel | Minimal kernel; other services run in user space via message passing |
| Protection | Controlling access to system resources |
| Security | Defending the system from external/internal attacks |
| Cloud computing | Delivering computing resources over the internet (IaaS/PaaS/SaaS) |
