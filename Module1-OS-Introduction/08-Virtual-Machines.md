# 8. Virtual Machines

Covers: "With a neat figure, explain the concept of virtual machines", "With a
neat diagram, explain the concept of the virtual machine", "With neat diagram,
explain virtual, non virtual and VM ware architecture", "Explain with a neat
diagram VM-WARE Architecture".

---

## 8.1 The Virtual Machine Concept

**Definition:** Virtualization abstracts the hardware of a single computer (CPU,
memory, disk, network cards, etc.) into several different execution
environments, each creating the illusion that it is running on its own private
computer.

**Points:**
1. These environments can be entirely different operating systems (e.g. Windows
   and Linux) running at the same time, able to interact with each other.
2. **Host OS** = the main OS actually installed on the physical hardware.
   **Guest OS** = an OS running inside a virtual machine, managed by the host.
3. A user can switch among different guest OSes the same way they'd switch
   between processes running concurrently within one OS.
4. Virtual machines first appeared as the **VM Operating System** for IBM
   mainframes in **1972** — allowing multiple users to run tasks concurrently on
   a system originally designed for one user.

### Diagram — Non-Virtual vs Virtual Machine
```
(a) Non-virtual machine:          (b) Virtual machine:
                                    processes    processes    processes
      processes                       |             |             |
         |                          kernel        kernel        kernel
   programming interface              VM1           VM2           VM3
         |                        ------------------------------------
       kernel                        virtual-machine implementation
         |                        ------------------------------------
      hardware                              hardware
```

---

## 8.2 Implementation

**Points:**
1. Hard to implement well — must provide an *exact duplicate* of the underlying
   machine, including its own user/kernel mode distinction.
2. The virtual-machine software (the hypervisor/VMM) itself runs in **kernel
   mode** (since it IS effectively an operating system). Each virtual machine
   it manages can only execute in **user mode**.

---

## 8.3 Benefits of Virtualization

**Points:**
1. **Shares the same hardware** to run several different OS environments
   concurrently.
2. **Isolation**: the host is protected from the VMs, and VMs are protected from
   each other — a virus in one guest OS corrupts only that guest, not the host
   or other guests.
3. VMs can still **share software resources** when needed: via a shared file
   system volume, or a virtual communication network between VMs.
4. **System development**: normally, testing OS changes requires taking the
   whole machine offline ("system development time"). With VMs, you can run
   production work in one VM while developing/testing in another, on the same
   physical hardware.
5. Enables **rapid cross-platform testing** — multiple guest OSes running
   concurrently let developers quickly port/test code across environments.
6. **System consolidation** — running what used to require 2+ physical machines
   on a single physical machine, each in its own VM.

---

## 8.4 VMware Example

**Definition:** VMware is a popular commercial virtualization application that
abstracts Intel x86 hardware into isolated virtual machines, running as a
user-level application on top of a **host OS**.

**Points:**
1. VMware runs on a host OS (e.g. Linux or Windows) and lets that host run
   several different **guest operating systems** concurrently, each as an
   independent VM.
2. The **virtualization layer** is VMware's core — it abstracts the physical
   hardware into isolated virtual machines, each with its own virtual CPU,
   memory, disk, and network interface.
3. The guest OS inside each VM believes it's running on real/bare hardware — but
   it's actually running inside a user-level application on the host.

### Diagram (VMware architecture)
```
 application   application    application     application
     |              |              |               |
            [guest OS: FreeBSD] [guest OS: WinNT] [guest OS: WinXP]
            (virtual CPU/memory/devices for each guest)
     ---------------------------------------------------------
                        virtualization layer
     ---------------------------------------------------------
                   host operating system (Linux)
     ---------------------------------------------------------
             hardware:   CPU   |   memory   |   I/O devices
```

---

## 8.5 The Java Virtual Machine (JVM) — a different kind of VM

**Definition:** Java achieves platform independence by compiling source code into
**Java bytecode**, which runs on a **Java Virtual Machine (JVM)** — a software
layer implemented separately for each real hardware/OS platform.

**Points:**
1. Java source → compiled by `javac` → **bytecode** stored in `.class` files.
2. JVM = **class loader** + **Java interpreter**. The class loader loads compiled
   `.class` files (from both the user's program and the Java API) and verifies
   their validity.
3. The JVM also implements **memory management and garbage collection**.
4. Because the *same* bytecode runs on any platform's JVM, Java programs are
   "compile once, run anywhere."

### Diagram
```
Java program .class files ---\
                               >--  class loader --> Java interpreter --> host system (Windows, Linux, etc.)
   Java API .class files -----/
```
