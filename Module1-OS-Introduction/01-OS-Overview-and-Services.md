# 1. What Operating Systems Do & OS Services

Covers: "Define Operating System", "Briefly explain what operating system do", "What
operating system goals", "List and explain the services provided by OS for the
user and efficient operation of system", "Discuss in detail about Operating System
structure" (services part), system programs.

---

## 1.1 What is an Operating System?

**Definition:** An operating system (OS) is system software that acts as an
intermediary between a computer user and the computer hardware — it manages the
hardware and lets users execute programs conveniently and efficiently.

**Points:**
1. A computer system has 4 components: **Hardware** (CPU, memory, I/O devices),
   **Operating System**, **Application programs** (word processors, compilers,
   browsers), and **Users** (people, machines, other computers).
2. The OS controls and coordinates use of hardware among the various applications
   and users.
3. **Analogy:** An OS is like a government — it performs no useful work by itself,
   it just provides an *environment* within which other programs can do useful work.
4. OS Goals: make the computer convenient to use (hide hardware complexity), use
   hardware efficiently, provide an easy interface, and act as a resource allocator.

### Diagram (4-layer system view)
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
```

---

## 1.2 Two Viewpoints: User View & System View

### User View (depends on type of user)
1. **Standalone PC/laptop user** — OS designed for ease of use and good
   performance; resource utilization isn't a priority (one user owns everything).
2. **Terminal users on a mainframe/minicomputer** (shared) — OS designed to
   **maximize resource utilization**, ensuring no single user hogs more than their
   fair share of CPU/memory/I/O.
3. **Workstation users on a network** — OS balances ease of use with resource/file
   sharing availability.
4. **Embedded systems** (washing machines, cars) — little to no user interaction;
   just status LEDs.
5. **Handheld device users** — OS designed for ease of use and performance per unit
   of battery life.
6. **Mobile users** (smartphones/tablets) — touch screen and voice-recognition
   interfaces (e.g. Siri) instead of keyboard/mouse.

### System View
1. **Resource allocator** — the OS manages CPU time, memory space, file-storage
   space, and I/O devices, which may have conflicting requests from different
   programs; the OS decides who gets what, to operate efficiently and fairly.
2. **Control program** — the OS manages execution of user programs to prevent
   errors and improper use of the computer, especially regarding I/O devices.

---

## 1.3 Operating System Services

**Definition:** An operating system provides an environment for program execution,
offering a set of services both to programs/users and for the system's own
efficient operation.

### Services helpful to the USER

1. **User Interface** — the way users issue commands: **CLI** (Command Line
   Interface, e.g. shells like `sh`, `csh`, `bash`), **GUI** (Graphical User
   Interface — windows, icons, mouse-driven), or **Batch** interface (commands +
   directives placed in a file, executed together).
2. **Program Execution** — the OS must load a program into memory, run it, and
   terminate it (normally or abnormally).
3. **I/O Operations** — the OS transfers data to/from I/O devices (keyboard,
   printer, files) via device drivers, since user programs can't directly control
   hardware for efficiency and protection reasons.
4. **File-System Manipulation** — services to create/delete files & directories,
   search, list contents, change permissions.
5. **Communications** — Inter-Process Communication (IPC) between processes, on
   the same machine (shared memory, message passing) or over a network.
6. **Error Detection** — detecting and handling hardware errors (power failure,
   memory error), I/O errors (parity error, no paper in printer), and program
   errors (division by zero, illegal memory access).

### Services helpful for EFFICIENT SYSTEM OPERATION

7. **Resource Allocation** — allocating CPU cycles, main memory, storage, and I/O
   devices among multiple users/jobs.
8. **Accounting** — tracking system activity/resource usage, for billing or
   statistics to optimize future performance.
9. **Protection and Security** — controlling access to resources in a multiuser
   system; preventing processes from interfering with each other or the OS;
   securing the system from outside attackers (passwords, etc.).

### Diagram
```
                 user and other system programs
    ┌──────────────────────────────────────────────────┐
    │   GUI    │   batch   │   command line             │
    │                 user interfaces                   │
    ├─────────────────────────────────────────────────── ┤
    │                   system calls                     │
    ├──────────────────────────────────────────────────  ┤
    │ program   I/O     file      communi-  resource      │
    │ execution operations systems  cation   allocation   │
    │                                        accounting   │
    │ error detection          protection and security     │
    │                      services                        │
    └──────────────────────────────────────────────────┘
                      operating system
                           |
                        hardware
```

---

## 1.4 User-Operating System Interfaces

### Command Interpreter (Shell)
**Definition:** A program that gets and executes user-typed commands (e.g. `sh`,
`csh`, `bash` in UNIX/Linux).

**Points:**
1. Many commands manipulate files: create, delete, list, copy, execute, etc.
2. Two implementation approaches:
   - The interpreter itself contains code for the command (direct jump to its
     routine).
   - The command's code lives in a separate file; the interpreter loads and
     executes that file, passing parameters.
3. Approach 2 makes it easy to add new commands without modifying the interpreter.

### Graphical User Interface (GUI)
**Definition:** A mouse-based window-and-menu interface, instead of typed commands.

**Points:**
1. Provides a **desktop metaphor** — icons represent programs, files, folders.
2. Clicking the mouse can invoke a program, select a file/folder, or open a menu.
3. Easier for beginners; CLI is often faster/more powerful for experienced users.

---

## 1.5 System Programs

**Definition:** System programs (system utilities) provide a convenient
environment for program development and execution, sitting between the user and
system calls.

**The 6 Categories:**
1. **File management** — create, delete, copy, rename, list files/directories.
2. **Status information** — date, time, number of users, memory/disk space,
   logging utilities.
3. **File modification** — text editors and other content-changing tools.
4. **Programming-language support** — compilers, assemblers, linkers, debuggers,
   interpreters.
5. **Program loading and execution** — loaders, dynamic loaders, interactive
   debuggers.
6. **Communications** — mail, web browsers, remote login, file transfer programs.
