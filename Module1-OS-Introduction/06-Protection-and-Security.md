# 6. Protection and Security

Covers: part of "Discuss the services that are provided by the operating systems",
general protection & security concepts for Module 1.

---

## 6.1 Protection

**Definition:** Protection is any mechanism for controlling the access of
processes or users to the resources defined by a computer system.

**Points:**
1. Needed because a computer system with multiple users/concurrent processes must
   regulate access to shared data, files, memory, CPU, and other resources.
2. Examples of hardware-enforced protection:
   - Memory-addressing hardware ensures a process executes only within its own
     address space.
   - The timer ensures no process can monopolize the CPU forever.
   - Device-control registers aren't accessible to users directly.
3. Protection improves **reliability** by detecting latent errors at interfaces
   between subsystems, preventing a malfunctioning subsystem from contaminating
   a healthy one.
4. A system can have adequate protection but still be insecure (e.g. a user's
   login credentials get stolen — their data can be copied/deleted even though
   file/memory protection mechanisms work correctly).

---

## 6.2 Security

**Definition:** Security is the job of defending a system from external and
internal attacks.

**Points:**
1. Attack types include: viruses and worms, denial-of-service attacks (exhaust
   system resources so legitimate users are locked out), identity theft, and
   theft of service (unauthorized use).
2. Some systems treat attack-prevention as an OS responsibility; others leave it
   to policy or additional security software.
3. Operating-system security is a fast-growing area given the rising frequency of
   security incidents.

---

## 6.3 User & Group Identification

**Points:**
1. Most OSes maintain a list of user names and associated **user identifiers
   (user IDs)** — in Windows, called a **Security ID (SID)**.
2. At login, the **authentication** stage determines the user's ID, which is then
   attached to all of that user's processes/threads.
3. **Groups**: to control access by sets of users (not just individuals), OSes
   define group names and **group identifiers (GIDs)** — a user can belong to
   multiple groups.
4. **Privilege escalation**: sometimes a user needs temporary extra permissions
   (e.g. to access a restricted device). On UNIX, the `setuid` attribute makes a
   program run with the file owner's user ID instead of the caller's — the
   process keeps this elevated privilege until it's turned off or the process
   terminates.
