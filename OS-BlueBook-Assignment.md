# Operating Systems: Blue Book Assignment

Subject: Operating Systems (BCS303) | Semester III | VTU | 5 questions x 10 marks

The mark split given in the question sheet is followed for every answer, so each part gets the space it needs.

---

## Q1. Define an operating system. Explain the services provided by an operating system and the dual-mode operation with a neat diagram. [10]

*Marks: Definition 1 + Services 5 + Dual-mode 4*

### Definition [1]

An operating system (OS) is system software that works as a middle layer between the user and the computer hardware. It manages the hardware and lets the user run programs in an easy and efficient way. Examples: Windows, Linux, Android.

```
      user 1     user 2     user 3  ...  user n
        |          |          |            |
   [ compiler | text editor | browser | database ]   <- application programs
                         |
                  OPERATING SYSTEM
                         |
              COMPUTER HARDWARE (CPU, memory, I/O)
```

### Services provided by an operating system [5]

The OS gives some services to the user and some services to keep the system running well.

**A. Services for the user**

1. **User interface**
   - The way a user talks to the computer.
   - Types: command line (CLI) like bash, graphical (GUI) like Windows, and batch interface.
2. **Program execution**
   - The OS loads a program into memory, runs it, and ends it, normally or because of an error.
3. **I/O operations**
   - A running program may need to read from the keyboard or write to a printer.
   - Users cannot control devices directly, so the OS does the I/O for them.
4. **File system manipulation**
   - Create, delete, read, write and search files and folders.
   - It also manages permissions of files.
5. **Communication**
   - Processes may need to exchange information, on the same computer or over a network.
   - The OS does this using shared memory or message passing.
6. **Error detection**
   - The OS keeps watching for errors in the CPU, memory, I/O devices and user programs (for example a power failure, no paper in the printer, divide by zero).
   - It takes a proper action so the system keeps working correctly.

**B. Services for efficient working of the system**

7. **Resource allocation**
   - When many users or programs run at the same time, the OS decides who gets the CPU, memory and devices.
8. **Accounting**
   - It keeps a record of which user uses how much of which resource. This is useful for billing and statistics.
9. **Protection and security**
   - Protection controls the access of processes to resources.
   - Security stops outsiders from using the system, usually with a password (authentication).

### Dual-mode operation [4]

**Definition:** Dual-mode operation means the hardware has two modes of execution, **user mode** and **kernel mode**, so that the OS is protected from the user programs.

**Points:**

1. A **mode bit** is added to the hardware. Kernel mode = 0, user mode = 1.
2. When a user program is running, the system is in user mode.
3. When the user program needs an OS service (for example, reading a file), it makes a **system call**. This is a trap, and the mode bit changes to kernel mode (0).
4. The OS does the work in kernel mode. After it finishes, the control goes back to the program and the mode bit is set to user mode (1).
5. At the time of booting, the hardware starts in kernel mode. Then the OS is loaded and starts the user applications in user mode.
6. Some instructions are **privileged instructions** (for example I/O, timer setting, interrupt management). They can run only in kernel mode. If a user program tries one, the hardware treats it as illegal and gives a trap to the OS.
7. **Why it is needed:** without it, a wrong or harmful program could damage the OS or other programs.
8. A **timer** is also used so that a user program cannot hold the CPU forever.

**Diagram:**

```
         USER MODE (mode bit = 1)
      +-----------------------------+
      |  user process executing     |
      |  ... calls a system call ...|
      +--------------+--------------+
                     |  trap : set mode bit = 0
                     v
      +-----------------------------+
      |  KERNEL MODE (mode bit = 0) |
      |  OS executes the system call|
      +--------------+--------------+
                     |  return from call : set mode bit = 1
                     v
      +-----------------------------+
      |  user process resumes       |
      +-----------------------------+
```

---

## Q2. Explain the types of system calls with examples. Analyze the layered, microkernel and modular structures, and justify which is most suitable for a real-time embedded system. [10]

*Marks: System calls 4 + Structure analysis 4 + Justification 2*

### System calls [4]

**Definition:** A system call is the way in which a user program asks the operating system to do some work for it. It is the interface between a running program and the OS.

**Points:**

1. A system call changes the mode from user mode to kernel mode.
2. Programmers usually use an **API** (like POSIX or Windows API) instead of calling the system call directly. This makes the program portable.
3. Parameters are passed to the OS in three ways: in registers, in a table in memory (and its address in a register), or on the stack.

**Types of system calls (6 types):**

| Type | What it does | Examples |
|---|---|---|
| 1. Process control | create, end, load, wait for processes, allocate memory | `fork()`, `exit()`, `wait()`, `exec()` |
| 2. File management | create, delete, open, close, read and write files | `open()`, `read()`, `write()`, `close()` |
| 3. Device management | request or release a device, read and write to it | `ioctl()`, `read()`, `write()` |
| 4. Information maintenance | get or set time, date and system data | `getpid()`, `time()`, `alarm()` |
| 5. Communication | create connection, send and receive messages, shared memory | `pipe()`, `shmget()`, `send()`, `recv()` |
| 6. Protection | set permissions of files and resources | `chmod()`, `chown()`, `umask()` |

### Structures of an operating system [4]

#### 1. Layered structure

**Definition:** The OS is divided into a number of layers. The bottom layer (layer 0) is the hardware and the top layer is the user interface. Each layer uses the services of only the lower layers.

```
   +---------------------+  layer N   user interface
   |         ...         |
   +---------------------+  layer 1
   +---------------------+  layer 0   hardware
```

- **Advantage:** simple to build and to debug. Each layer is tested before the next one is made.
- **Disadvantage:** hard to decide the layers properly. It is slow, because a request has to go through all the layers.

#### 2. Microkernel structure

**Definition:** Only the very necessary parts (process management, memory management and communication) are kept in the kernel. All other services, such as file system and device drivers, run in user space.

```
 user mode :  [application] [file system] [device driver]
                    ^ messages ^ messages ^
 kernel mode: [ microkernel : IPC, memory, scheduling ]
                             |
                         hardware
```

- **Advantage:** small kernel, easy to extend, more secure and reliable. If a service crashes, the kernel keeps working.
- **Disadvantage:** the communication through message passing between user space and kernel space makes it slower.
- Example: Mach (used in macOS), QNX.

#### 3. Modular structure

**Definition:** The kernel has a small core, and other parts are loaded as modules when they are required (loadable kernel modules). This is the method used by most modern systems.

```
        +---------+  +---------+  +---------+
        | file    |  | device  |  | network |
        | system  |  | driver  |  | module  |
        +----+----+  +----+----+  +----+----+
             |            |            |
          +--+------------+------------+--+
          |          CORE KERNEL          |
          +-------------------------------+
```

- **Advantage:** flexible, and it is efficient because modules call each other directly without message passing.
- **Disadvantage:** a module is inside the kernel, so a bug in one module can affect the whole system.
- Example: Linux, Solaris.

**Comparison:**

| Point | Layered | Microkernel | Modular |
|---|---|---|---|
| Kernel size | Large | Very small | Small core |
| Speed | Slow | Slower (messages) | Fast |
| Reliability | Medium | High | Medium |
| Flexibility | Low | High | High |

### Justification for a real-time embedded system [2]

**Most suitable: Microkernel.**

1. A real-time system must respond within a fixed time, and it must be very reliable. A microkernel is small, so its behaviour is easier to predict and test.
2. If one driver or service fails, the kernel and the other services keep running. This is important in cars, medical devices and aircraft.
3. Embedded devices have little memory, and a microkernel needs less memory because only the needed services are added.
4. Examples of real-time systems that use a microkernel are QNX and VxWorks.
5. The message passing makes it a little slower, but good design and fast hardware reduce this problem. The layered structure is too slow, and the modular structure is less safe because a bug in a module can crash the whole kernel.

---

## Q3. Explain the process state diagram and the PCB. Trace the following program, draw the process tree and state how many times "Hello" is printed. [10]

```c
int main() {
    fork();
    fork();
    printf("Hello");
}
```

*Marks: States 3 + PCB 3 + Trace and tree 4*

### Process states [3]

**Definition:** A process is a program under execution. As it runs, it changes its state. A process can be in one of 5 states.

1. **New** : the process is being created.
2. **Ready** : the process has everything it needs and is waiting for the CPU.
3. **Running** : the instructions of the process are being executed by the CPU.
4. **Waiting** : the process is waiting for some event, like I/O completion or a signal.
5. **Terminated** : the process has finished its execution.

**Process state diagram:**

```
                    interrupt (time slice over)
                 +--------------------------------+
                 |                                |
                 v                                |
  +-----+   admitted   +-------+  scheduler   +---+-----+   exit   +------------+
  | NEW | ------------> | READY | -----------> | RUNNING | -------> | TERMINATED |
  +-----+               +-------+   dispatch   +---+-----+          +------------+
                            ^                      |
                            |                      | I/O or event wait
                            |    I/O or event      v
                            |    completion    +---------+
                            +------------------| WAITING |
                                               +---------+
```

Transitions:

- New to Ready : the process is admitted.
- Ready to Running : the scheduler dispatches it.
- Running to Ready : an interrupt (the time slice is over).
- Running to Waiting : the process asks for I/O or waits for an event.
- Waiting to Ready : the I/O or the event is completed.
- Running to Terminated : the process exits.

### Process Control Block (PCB) [3]

**Definition:** The PCB is a data structure kept by the OS for every process. It stores all the information about that process. It is also called the task control block.

**Contents of the PCB:**

1. **Process state** : new, ready, running, waiting, terminated.
2. **Process number (ID)** : the unique id of the process.
3. **Program counter** : the address of the next instruction to be executed.
4. **CPU registers** : accumulators, index registers, stack pointers. They are saved when an interrupt occurs, so the process can continue later.
5. **CPU scheduling information** : priority and pointers to scheduling queues.
6. **Memory management information** : base and limit registers, page tables or segment tables.
7. **Accounting information** : CPU time used, time limits, process numbers.
8. **I/O status information** : list of I/O devices given to the process, list of open files.

```
   +----------------------+
   |    process state     |
   +----------------------+
   |    process number    |
   +----------------------+
   |    program counter   |
   +----------------------+
   |      registers       |
   +----------------------+
   |    memory limits     |
   +----------------------+
   |    list of open files|
   +----------------------+
   |         ...          |
   +----------------------+
```

The PCB is used in **context switching**. When the CPU switches from one process to another, the state of the old process is saved in its PCB, and the state of the new process is loaded from its PCB.

### Trace of the program, process tree and output [4]

**Facts about `fork()`:** it creates a copy of the calling process (the child). After `fork()`, both the parent and the child continue from the next line. The child gets return value 0 and the parent gets the child's pid.

**Trace:**

1. Initially there is 1 process, call it **P0**.
2. After the **first `fork()`**: P0 creates a child **P1**. Now there are 2 processes, both at the second `fork()`.
3. The **second `fork()`** is run by both processes:
   - P0 creates **P2**.
   - P1 creates **P3**.
   Now there are 4 processes.
4. All 4 processes reach `printf("Hello")` and each one prints it.

**Process tree:**

```
                    P0
                  /    \
         (fork 1)/      \(fork 2)
                P1       P2
                |
        (fork 2)|
                P3
```

| Process | Created by | Created at |
|---|---|---|
| P0 | main program | start |
| P1 | P0 | first fork |
| P2 | P0 | second fork |
| P3 | P1 | second fork |

**Number of times "Hello" is printed = 4.**

**Rule:** for n `fork()` calls one after the other, the total number of processes is 2^n. Here n = 2, so 2^2 = 4 processes, and "Hello" is printed 4 times. (Since there is no `\n` and no `wait()`, the order of the 4 outputs is not fixed.)

I ran this program, and the output was Hello four times.

---

## Q4. Explain the multithreading models with diagrams. Analyze many-to-one versus one-to-one for a web server handling thousands of requests. [10]

*Marks: Models 5 + Web server analysis 5*

### Multithreading models [5]

**Definition:** A thread is the basic unit of CPU use. It has a thread id, a program counter, a register set and a stack. Threads of the same process share the code, data and files. A process with many threads is called a multithreaded process.

There are two kinds of threads:

- **User threads** : managed by a thread library in user space, without kernel support.
- **Kernel threads** : managed directly by the operating system.

A relationship must exist between user threads and kernel threads. There are three models for this.

#### 1. Many-to-One model

Many user threads are mapped to a single kernel thread.

```
   user threads :   ~     ~     ~     ~
                     \     \   /     /
                      \     \ /     /
                       +-----+-----+
                             |
   kernel thread :          (k)
```

- **Advantage:** thread management is done in user space by the library, so it is efficient (fast and cheap).
- **Disadvantages:**
  - If one thread makes a blocking system call, the **whole process is blocked**.
  - Many threads cannot run in parallel on a multiprocessor, because only one thread can use the kernel at a time.
- Examples: Solaris Green threads, GNU Portable Threads.

#### 2. One-to-One model

Each user thread is mapped to its own kernel thread.

```
   user threads :   ~     ~     ~     ~
                    |     |     |     |
   kernel threads: (k)   (k)   (k)   (k)
```

- **Advantages:**
  - More concurrency: if one thread blocks, the others can still run.
  - Many threads can run in parallel on a multiprocessor.
- **Disadvantage:** creating a user thread needs creating a kernel thread, which is costly. So the number of threads is usually limited.
- Examples: Linux, Windows.

#### 3. Many-to-Many model

Many user threads are multiplexed to a smaller or equal number of kernel threads.

```
   user threads :   ~     ~     ~     ~
                     \     \   /     /
                      \     \ /     /
   kernel threads:    (k)   (k)   (k)
```

- **Advantages:**
  - The programmer can create as many user threads as needed.
  - The kernel threads can run in parallel on a multiprocessor.
  - If one thread blocks, the kernel can schedule another thread.
- **Two-level model:** this is a variation of many-to-many, where a user thread can also be bound to one kernel thread.
- Examples: older versions of Solaris, HP-UX.

**Summary:**

| Model | Parallelism | Blocking call | Cost |
|---|---|---|---|
| Many-to-One | No | Blocks the whole process | Low |
| One-to-One | Yes | Blocks only that thread | High |
| Many-to-Many | Yes | Others still run | Medium |

### Many-to-one vs one-to-one for a web server [5]

A web server gets thousands of requests at the same time. A new thread is usually created for each request. Some requests will block for a long time, for example waiting for a database or a disk.

| Point | Many-to-One | One-to-One |
|---|---|---|
| Blocking request | One blocked request blocks **all** requests, because the whole process is blocked | Only that thread is blocked, the other requests continue |
| Use of many CPUs | Only one CPU is used, so it cannot use a multi-core server | Threads run on different cores in parallel |
| Speed of creating threads | Very fast (done in user space) | Slower, because each one needs a kernel thread |
| Memory use | Low | High, each thread has a kernel structure and a stack |
| Number of threads | Can be very large | Limited by the system, thousands of threads may cause overhead |
| Response time for users | Poor under heavy load | Good |

**Analysis:**

1. In a web server, a lot of requests wait for I/O. With many-to-one, one blocking system call makes the whole server stop for all clients. This is the biggest problem, and it makes the server unsuitable.
2. A modern server has many cores. Many-to-one cannot use them, so the throughput stays low. One-to-one gives true parallelism.
3. The weak point of one-to-one is the cost of creating a kernel thread for each request. A server with thousands of requests may create too many threads and run out of memory.
4. This problem is solved by using a **thread pool**: a fixed number of threads is created at the start and reused for the requests. So the creation cost and the number of threads are controlled.

**Conclusion:** One-to-one is the better model for a web server handling thousands of requests, together with a thread pool. If the server needs a very large number of threads, many-to-many can also be a good choice.

---

## Q5. Explain the two models of inter-process communication (shared memory and message passing) with diagrams. Compare them and justify which model suits (a) two processes on the same machine exchanging large data, and (b) processes on different machines in a distributed system. [10]

*Marks: Need 1 + Shared memory 3 + Message passing 3 + Comparison 1 + Justification 2*

### Need for IPC [1]

Processes in a system are either **independent** (they do not affect other processes) or **cooperating** (they affect or are affected by other processes). Cooperating processes need to exchange data, and the OS gives them inter-process communication (IPC). The reasons are:

1. **Information sharing** : many processes may need the same file or data.
2. **Computation speedup** : a big task is split into sub-tasks that run in parallel.
3. **Modularity** : a system is divided into separate cooperating modules.
4. **Convenience** : a single user can work on many tasks at the same time.

There are two models of IPC: **shared memory** and **message passing**.

### Shared memory model [3]

**Definition:** A region of memory is shared by the cooperating processes. They exchange information by reading and writing data in this region.

**Points:**

1. The shared region is created in the address space of one process. The other processes attach it to their own address space.
2. A system call is needed only to create the shared region. After that, all accesses are normal memory accesses, so it is **fast**.
3. The processes are responsible for the form of the data and the location. The OS does not control them.
4. The processes must make sure that they do not write to the same location at the same time (they need synchronization).
5. Good for large amounts of data.

**Producer-consumer example:** one process produces data and puts it in a shared buffer. The other process consumes (takes) it. A **bounded buffer** of a fixed size is used as a circular array with two pointers `in` and `out`.

- Buffer is full when `(in + 1) % BUFFER_SIZE == out`. The producer must wait.
- Buffer is empty when `in == out`. The consumer must wait.

```
        +-----------------+
        |    Process A    |---- writes ---+
        +-----------------+               v
        +-----------------+        +-------------+
        |   Shared region |<-------|   (memory)  |
        +-----------------+        +-------------+
        +-----------------+               ^
        |    Process B    |---- reads ----+
        +-----------------+
        +-----------------+
        |      Kernel     |   (not involved after setup)
        +-----------------+
```

### Message passing model [3]

**Definition:** The processes communicate by sending and receiving messages, without sharing any address space. The OS provides two operations: `send(message)` and `receive(message)`.

**Points:**

1. A communication link has to be set up between the two processes first.
2. The OS (kernel) is used for every send and receive, so it is **slower**.
3. It is easier to use because the OS handles the details, and it works well for **small data**.
4. It is useful in a **distributed system**, where processes are on different computers.
5. A link can be made in different ways:
   - **Naming:** *direct* communication, `send(P, message)` and `receive(Q, message)`, where the processes name each other. *Indirect* communication uses a **mailbox** (port), `send(A, message)` and `receive(A, message)`.
   - **Synchronization:** *blocking* (synchronous) or *non-blocking* (asynchronous) send and receive.
   - **Buffering:** the message queue can be zero capacity, bounded capacity or unbounded capacity.

```
        +-----------+                    +-----------+
        | Process A |                    | Process B |
        +-----+-----+                    +-----+-----+
              | 1. send(message)               ^ 2. receive(message)
              v                                |
        +-----+--------------------------------+-----+
        |                   KERNEL                   |
        |            (message queue, link)           |
        +--------------------------------------------+
```

### Comparison [1]

| Point | Shared memory | Message passing |
|---|---|---|
| Method | Common memory region | send and receive of messages |
| Speed | Fast (no system call after setup) | Slow (system call for every message) |
| Data size | Good for large data | Good for small data |
| Kernel involvement | Only at the start | In every transfer |
| Synchronization | Done by the programmer | Done by the OS (blocking/non-blocking) |
| Distributed system | Hard to use | Easy to use |

### Justification [2]

**(a) Two processes on the same machine exchanging large data: Shared memory.**

- Both processes are on one computer, so they can share a memory region.
- After the setup, the data is read and written at normal memory speed, with no system call and no copying of the data through the kernel.
- With message passing, the large data would be copied again and again through the kernel, which is slow and wastes CPU time.

**(b) Processes on different machines in a distributed system: Message passing.**

- Different machines do not have common memory, so a shared region cannot be created.
- Message passing sends the data through the network and does not need shared address space.
- It is simple to set up and the OS handles the details. It also avoids the problem of two processes writing at the same time.
