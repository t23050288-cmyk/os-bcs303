# 5. Resource Management: Process, Memory, Storage & Cache

Covers: "List the responsibilities of the operating system for process management
and memory management", "Describe the structure of operating system and its
operations" (resource mgmt side), "What is caching?".

---

## 5.1 Process Management

**Definition:** A process is a **program in execution** — an active entity (unlike
the program itself, which is a passive entity like a file on disk).

**Points:**
1. A process needs resources (CPU time, memory, files, I/O devices) to accomplish
   its task; these are allocated when the process is created or at run-time.
2. A **single-threaded** process has one program counter and executes
   sequentially. A **multithreaded** process has multiple program counters, one
   per thread.
3. OS responsibilities for process management:
   - Creating and deleting both user and system processes
   - Scheduling processes/threads on the CPU
   - Suspending and resuming processes
   - Providing mechanisms for process synchronization
   - Providing mechanisms for process communication (IPC)

---

## 5.2 Memory Management

**Definition:** Main memory is a large array of bytes/words, each with its own
address — a repository of fast, directly-accessible data shared by the CPU and
I/O devices.

**Points:**
1. The CPU can only directly address/access **main memory** and registers — data
   from disk must first be transferred into main memory before processing.
2. For a program to run, it must be mapped to addresses and loaded into memory.
3. OS responsibilities for memory management:
   - Keeping track of which parts of memory are used and by which process
   - Allocating and deallocating memory space as needed
   - Deciding which processes/data to move into and out of memory

---

## 5.3 File-System Management

**Definition:** The OS abstracts physical storage devices into a logical storage
unit called a **file**, giving users a uniform, logical view of information
storage.

**Points:**
1. A file is a collection of related information defined by its creator —
   programs, data, text, binary, etc.
2. Files are organized into **directories** for ease of use; access control
   (read/write/append) can be applied per user.
3. OS responsibilities for file management:
   - Creating and deleting files and directories
   - Supporting primitives to manipulate files/directories
   - Mapping files onto mass storage
   - Backing up files onto stable (nonvolatile) storage media

---

## 5.4 Mass-Storage Management

**Definition:** Secondary storage (HDDs, NVM/SSD) backs up main memory, holding
programs and data permanently; tertiary storage (tape, optical disks) handles
backups/archival.

**Points:**
1. OS responsibilities: mounting/unmounting, free-space management, storage
   allocation, disk scheduling, partitioning, protection.
2. Since secondary storage is used constantly, its performance strongly affects
   overall system speed.
3. Tertiary storage management (less performance-critical) may be handled by the
   OS or left to applications: mounting media, allocating devices, migrating
   data between secondary and tertiary storage.

---

## 5.5 Cache Management

**Definition:** Caching copies frequently-used data from a slower storage system
into a faster, temporary one (the cache) so future accesses are quick.

**Points:**
1. Check the cache first; if the data is there ("hit"), use it directly; if not
   ("miss"), fetch from the source and also cache a copy for next time.
2. Internal CPU **registers** act as a high-speed cache for main memory —
   compilers decide what to keep in registers vs memory.
3. Hardware-only caches (instruction cache, data cache) aren't managed by the OS
   at all.
4. **Cache management is a design problem**: careful choice of cache size and
   replacement policy greatly affects performance.
5. Data movement across levels can be **explicit** (OS-controlled, e.g.
   disk→memory) or **implicit** (hardware-controlled, e.g. cache→register).
6. In a multiprocessor system with per-CPU local caches, keeping all cached
   copies of the same data consistent is called **cache coherency** — usually a
   hardware-level concern.

---

## 5.6 I/O System Management

**Definition:** The I/O subsystem hides device peculiarities from the rest of the
OS and from users.

**Points:**
1. Consists of: a memory-management component (buffering, caching, spooling), a
   general device-driver interface, and drivers for specific hardware devices.
2. Only the **device driver** knows the specific quirks of the device it's
   assigned to — everything above it uses a uniform interface.
