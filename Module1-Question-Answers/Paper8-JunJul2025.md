# BCS303 — June/July 2025 Exam
## Module 1: Introduction to Operating Systems

> Note: Two identical copies of this exact paper were sent — this file covers
> both.

---

## Q.1 a) Define operating system. Briefly explain what operating system do. [6]

### Definition
An OS is system software that acts as an intermediary between a computer user
and the computer hardware.

### What OS Do
1. Manages 4 components: hardware, OS, application programs, users.
2. Controls hardware and coordinates its use among applications/users.
3. Acts as a resource allocator (CPU, memory, storage, I/O) and a control
   program (prevents errors/improper use).
4. Like a government — provides an *environment* for other programs to do work.

---

## Q.1 b) What is caching? List and explain performance of various levels of storage. [8]

### Definition
Caching copies frequently-used data from a slower storage system into a faster,
temporary one (the cache), so future accesses are quick.

### Storage Hierarchy (fastest/smallest → slowest/largest)
```
        registers        <- fastest, smallest, volatile
          cache
       main memory
   ─────────────────────  (volatile above, nonvolatile below)
   nonvolatile memory (SSD/NVM)
      hard-disk drives
        optical disk
       magnetic tapes      <- slowest, largest, nonvolatile
```

### Points
1. As you move down: capacity increases, access speed decreases, cost per byte
   decreases.
2. If data is in the cache ("hit") it's used directly; if not ("miss"), it's
   fetched from the source and also cached for next time.
3. Cache management (size, replacement policy) is critical to performance.

---

## Q.1 c) What are the different special purpose system? List them and explain each in brief. [6]

### Multimedia Systems
Handle audio/video; data (e.g. video frames) must be delivered under time
restrictions (e.g. 30 fps). Examples: MP3, DVD, video conferencing.

### Handheld Systems
PDAs, smartphones. Face challenges: limited memory, slower (power-saving)
processors, small screens — but succeed due to portability and convenience.

---

## Q.2 a) Explain different operating system services which are helpful to the user. [6]

### Points
1. User Interface (CLI/GUI/batch)
2. Program Execution
3. I/O Operations
4. File-System Manipulation
5. Communications (IPC)
6. Error Detection

---

## Q.2 b) Define system calls. Explain with example how system calls are used. [8]

### Definition
A system call is the interface through which a user program requests a service
from the OS.

### Example — copying a file
```
Acquire input file name (syscall: write prompt, accept input)
Acquire output file name (syscall: write prompt, accept input)
Open the input file (syscall) -> abort if it doesn't exist (syscall)
Create output file (syscall) -> abort if it exists (syscall)
Loop: Read from input file (syscall), Write to output file (syscall)
Until read fails
Close output file (syscall)
Write completion message (syscall)
Terminate normally (syscall)
```
Even a simple 2-file program needs a dozen+ system calls.

---

## Q.2 c) Discuss in detail about Operating System structure. [6]

### Points
1. **Simple structure** (MS-DOS) — no layer separation, risky.
2. **Layered approach** — layers use only lower layers; simple to debug, less
   efficient.
3. **Microkernels** — minimal kernel + user-space services via message passing.
4. **Modules** — small kernel + modules that call each other directly.
5. **Hybrid** — most modern OSes combine multiple structures.
