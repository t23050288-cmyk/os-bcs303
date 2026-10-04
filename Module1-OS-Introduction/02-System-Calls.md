# 2. System Calls

Covers: "Define system call. List the types of system calls", "What are system
calls? Explain all types of system calls", "Define system calls. Explain with
example how system calls are used", "Explain types of system calls provided by
operating system".

---

## 2.1 What is a System Call?

**Definition:** A system call is the programming interface through which a user
program requests a service from the operating system — it is the mechanism a
process uses to ask the kernel to do something on its behalf.

**Points:**
1. Usually written in C/C++ (some performance-critical parts in assembly).
2. Invoked as a **trap** to a specific location in the interrupt vector; the mode
   bit switches from user mode (1) to kernel mode (0) during execution.
3. Most programmers don't call system calls directly — they use an **Application
   Programming Interface (API)**, e.g. the Windows API, POSIX API (UNIX/Linux),
   or Java API. The API internally makes the appropriate system calls.
4. Benefit of using an API instead of raw system calls: **greater program
   portability** across systems — your code calls `fopen()` and the API/runtime
   maps that to the right system call for the underlying OS.
5. Each system call has a unique number; a **system call table** maps numbers to
   the address of each service routine.

### Example — copying a file (illustrates the sequence of system calls needed)
```
Acquire input file name   -> write prompt to screen (syscall), accept input (syscall)
Acquire output file name  -> write prompt to screen (syscall), accept input (syscall)
Open the input file        -> if file doesn't exist, abort (syscall)
Create output file         -> if file exists, abort (syscall)
Loop:
    Read from input file (syscall)
    Write to output file (syscall)
Until read fails
Close output file (syscall)
Write completion message to screen (syscall)
Terminate normally (syscall)
```
Even a "simple" 2-file-copy program involves a dozen+ individual system calls.

---

## 2.2 How Parameters Are Passed to the OS

**Points (3 general methods):**
1. **Pass parameters in registers** — simplest, but registers are limited in
   number/size.
2. **Parameters stored in a block (table) in memory**, and the **address of the
   block** is passed in a register — used by Linux and Solaris.
3. **Push parameters onto the stack** by the program; the OS **pops them off the
   stack**.

---

## 2.3 Types of System Calls (6 Categories)

**Easy way to remember:** *Process, File, Device, Information, Communication,
Protection.*

### 1. Process Control
- `end`, `abort`, `load`, `execute`, `create process`, `terminate process`
- `get/set process attributes` (priority, max execution time)
- `wait for time`, `wait event`, `signal event`
- `allocate and free memory`

### 2. File Management
- `create file`, `delete file`, `open`, `close`
- `read`, `write`, `reposition` (seek)
- `get/set file attributes` (name, type, permissions)

### 3. Device Management
- `request device`, `release device`
- `read`, `write`, `reposition`
- `get/set device attributes`
- `logically attach or detach devices`

### 4. Information Maintenance
- `get/set time or date`
- `get/set system data`
- `get/set process, file, or device attributes`

### 5. Communications
- `create, delete communication connection`
- `send, receive messages`
- `transfer status information`
- `attach or detach remote devices`
- Two models: **message passing** (simpler, good for small data, more system
  calls needed) vs **shared memory** (faster for large data, harder to implement,
  fewer system calls).

### 6. Protection
- Adjust access-control mechanisms for resources.
- Grant temporary elevated permissions to non-privileged users under controlled
  conditions.

### Example (one call per category, with an example each)
| Category | Example call | Example use |
|---|---|---|
| Process Control | `fork()` | Create a new child process |
| File Management | `open()` | Open a file for reading |
| Device Management | `ioctl()` | Configure a device |
| Information Maintenance | `getpid()` | Get current process ID |
| Communications | `pipe()` | Create an IPC channel between processes |
| Protection | `chmod()` | Change a file's access permissions |
