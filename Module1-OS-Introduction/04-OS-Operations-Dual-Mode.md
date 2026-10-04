# 4. Operating-System Operations: Multiprogramming, Multitasking & Dual-Mode

Covers: "Explain multi programming and time sharing systems", "Explain the dual
mode operation in operating systems with a neat block diagram", "What is dual
mode operation and what is the need of it?".

---

## 4.1 Multiprogramming

**Definition:** Multiprogramming increases CPU utilization by organizing jobs so
the CPU **always has something to execute** — several processes are kept in
memory at once.

**Points:**
1. A single program alone cannot keep the CPU **or** I/O devices busy 100% of the
   time (it has to wait for I/O sometimes).
2. The OS keeps several jobs in memory simultaneously; this set is a subset of
   the larger **job pool** kept in secondary storage.
3. When the running job needs to **wait** (e.g. for I/O), the OS switches the CPU
   to another job instead of leaving it idle.
4. As long as at least one job is ready to run, the CPU is **never idle**.
5. **Analogy:** A lawyer with multiple clients works on another case while one
   is waiting for papers — never idle for lack of work.
6. Multiprogramming improves resource utilization but does **not** by itself
   provide for interactive user response.

### Diagram (memory layout)
```
0 ┌────────────────────┐
  │   operating system  │
  ├────────────────────┤
  │       job 1         │
  ├────────────────────┤
  │       job 2         │
  ├────────────────────┤
  │       job 3         │
  ├────────────────────┤
  │       job 4         │
512M└────────────────────┘
```

---

## 4.2 Multitasking (Time-Sharing)

**Definition:** Multitasking (time-sharing) is a logical extension of
multiprogramming — the CPU switches among multiple processes **so frequently**
that users get the illusion of simultaneous execution and fast interactive
response.

**Points:**
1. Requires an **interactive (hands-on)** system — direct user-system
   communication via keyboard/mouse, with results shown quickly.
2. **Response time** should be short — typically under 1 second.
3. Each user feels like they have the whole system to themselves, even though
   it's shared among many users.
4. Needs **memory management** (several processes in memory at once),
   **CPU scheduling** (deciding which ready process runs next), and
   **virtual memory** (lets a process run even if not entirely in memory — allows
   programs larger than physical memory to run).
5. **Virtual memory** separates **logical memory** (what the programmer sees) from
   **physical memory** (actual RAM) — frees programmers from worrying about
   memory limits.

---

## 4.3 Dual-Mode (and Multimode) Operation

**Definition:** A hardware-supported mechanism with (at least) two modes of
execution — **user mode** and **kernel mode** — used to protect the OS from
errant/malicious user programs, and protect users from each other.

**Points:**
1. A **mode bit** in hardware indicates the current mode: kernel = **0**, user =
   **1**.
2. When the system executes a user application, it's in **user mode**. When a
   user program requests an OS service (via a **system call**), the system
   **traps** into **kernel mode** to fulfill the request.
3. At boot time, hardware starts in **kernel mode**; the OS loads and then starts
   user applications in **user mode**.
4. Whenever a **trap or interrupt** occurs, hardware automatically switches to
   kernel mode (mode bit → 0).
5. **Privileged instructions** (I/O control, timer management, interrupt
   management, mode switching) can **only** execute in kernel mode. If user mode
   code attempts one, hardware treats it as illegal and traps to the OS.
6. **Why needed:** without this separation, a buggy or malicious user program
   could directly manipulate hardware, corrupt other programs, or crash the
   whole system (this is exactly MS-DOS's weakness — no dual-mode protection).
7. Extended further in real hardware: Intel CPUs have **4 protection rings**
   (ring 0 = kernel, ring 3 = user); ARMv8 has 7 modes; virtualization-capable
   CPUs add a separate mode for the hypervisor/VMM.

### Diagram (transition between modes)
```
 user process:  [user process executing] -> calls system call -> [return from system call]
                        (mode bit = 1 = USER MODE)
                              |  trap, mode bit -> 0        ^ return, mode bit -> 1
                              v                              |
 kernel:                [execute system call] ----------------
                        (mode bit = 0 = KERNEL MODE)
```

**Smallest example:** opening a file (`fopen`) looks like ordinary code to the
programmer, but internally it executes a `trap`, switches to kernel mode, the
kernel's file-system code runs the `open()` system call, then control returns to
user mode right after the call.

---

## 4.4 The Timer

**Definition:** A hardware timer interrupts the computer after a set period,
ensuring the OS never permanently loses control of the CPU to a runaway user
program (e.g. stuck in an infinite loop).

**Points:**
1. Implemented via a fixed-rate clock + a counter; the counter decrements on
   every clock tick, and an interrupt fires when it reaches 0.
2. Before giving control to a user program, the OS always sets the timer.
3. If the timer interrupts, control automatically returns to the OS, which can
   terminate the offending program or just give it more time.
4. Instructions that modify the timer are **privileged** (kernel-mode only).
