

# 🥶 Unit 4: Deadlocks (The System Freeze)

## 💀 Topic 1: Definition and Necessary Conditions for Deadlock

### **Introduction: The Fatal Embrace** 🤗

Imagine two cars meeting head-on in a narrow one-lane tunnel. Neither can move forward, and neither can back up. They are permanently blocked, or **deadlocked**. In an OS, a **deadlock** is a state where a set of processes are permanently blocked because each process is waiting for a resource held by another process in the set.

### **Core Concepts and Definitions** 📖

* **Deadlock Definition:** A situation where two or more processes are waiting indefinitely for an event that can only be caused by one of the waiting processes.
* **System Resources:** Deadlocks involve two main types of resources:
    1.  **Pre-emptable:** Can be taken away from the process holding it (e.g., CPU, memory). Deadlocks rarely involve pre-emptable resources.
    2.  **Non-pre-emptable:** Cannot be taken away without causing the computation to fail (e.g., printer, tape drive, lock/semaphore). Deadlocks primarily involve non-pre-emptable resources.

### **Necessary and Sufficient Conditions (Coffman Conditions)** 📜

For a deadlock to exist, **all four** of these conditions must hold true simultaneously. Think of them as the "Four Horsemen" of Deadlock.

| Condition | Explanation | Analogy |
| :--- | :--- | :--- |
| **1. Mutual Exclusion** 🚫 | At least one resource must be **non-sharable**. Only one process can use that resource at a time. | A single-use tool (e.g., a pen). |
| **2. Hold and Wait** ✋ | A process must be currently **holding** at least one resource while simultaneously **waiting** to acquire additional resources held by other processes. | Holding your keys while waiting for your friend's car to drive. |
| **3. No Pre-emption** 🙅 | A resource cannot be forcibly taken away from a process. It can only be released **voluntarily** by the process that is holding it, after the process has completed its task. | An already printed document cannot be unprinted and given back as blank paper. |
| **4. Circular Wait** ⭕ | A set of waiting processes {$P_0, P_1, P_2, \dots, P_n$} must exist such that $P_0$ is waiting for a resource held by $P_1$, $P_1$ is waiting for a resource held by $P_2$, $\dots$, and $P_n$ is waiting for a resource held by $P_0$. | A circular relay race where each runner is waiting for the baton (resource) held by the runner ahead of them. |



### **Important Keywords** 📌

* **Non-pre-emptable:** Key characteristic of resources involved in deadlock.
* **Resource Allocation Graph (RAG):** A directed graph used to visually model deadlocks. A **cycle** in the RAG is a necessary (but not always sufficient) condition for deadlock.

### **Common Mistakes to Avoid** ❌

* **Misunderstanding RAG Cycles:** A cycle in the RAG means deadlock **may** exist. If each resource type has only one instance, a cycle **guarantees** deadlock. If a resource type has multiple instances, a cycle **does not** guarantee deadlock.

---

## 🛡️ Topic 2: Deadlock Prevention

### **Introduction: Breaking the Cycle** 💔

**Deadlock Prevention** is a set of methods that ensures, by design, that **at least one of the four necessary conditions can never hold**. This ensures deadlock will never occur, but often at the cost of low resource utilization.

#### **1. Breaking Mutual Exclusion (Condition 1)** 🤝

* **Action:** Require all resources to be **sharable**.
* **Problem:** This is usually **impossible** for non-sharable devices like a printer or a tape drive.
* **Practical Application:** Spooling a printer (sending print jobs to a queue on a disk, a sharable resource) rather than giving a process exclusive access to the physical printer.

#### **2. Breaking Hold and Wait (Condition 2)** ⏱️

We can break this condition in two main ways:

* **Method A: Request All Resources Upfront:** A process must request **all** the resources it will ever need **before** starting execution.
    * **Pros:** Guarantees no 'Hold and Wait'.
    * **Cons:** Very low resource utilization (a process holds a resource for hours even if it only needs it for a minute at the end). Also leads to process **starvation** (a resource-heavy process might never get to run).
* **Method B: Release All Before Requesting More:** A process must release **all** its currently held resources before requesting any new ones.
    * **Pros:** Prevents holding old resources while waiting for new ones.
    * **Cons:** The state of the released resources (like a partially written file) might be lost or inconsistent.

#### **3. Breaking No Pre-emption (Condition 3)** ⚔️

* **Action:** Allow the OS to **forcibly take away** a resource from a process.
* **Procedure:**
    1.  If a process requests a resource that is currently held by another process, the OS checks if the resource is pre-emptable.
    2.  If the resource is held by a waiting process, the OS pre-empts it, taking the resource and giving it to the requesting process.
    3.  If the resource is held by a running process, the OS might also pre-empt it and force the victim process to **roll back** (restart) to a safe state.
* **Problem:** Only practical for resources whose state can be easily saved and restored (like CPU registers). Inconsistent for resources like printers or databases.

#### **4. Breaking Circular Wait (Condition 4)** 🔢

* **Action:** Impose a **total ordering** (ranking) on all resource types. Processes must request resources in an **increasing order of enumeration**.
* **Procedure:**
    1.  Assign a unique number to every resource type (e.g., Disk Drive = 1, Printer = 2, Tape Drive = 3).
    2.  A process currently holding resource $R_i$ can only request resource $R_j$ if $F(R_j) > F(R_i)$ (where $F$ is the numbering function).
* **Pros:** Simple to implement and guarantees that a circular chain of waiting can never form.
* **Cons:** Poor resource utilization (a process might need resource 3 first, but must request and hold resource 1 and 2 just to get permission). Difficult to maintain the optimal ordering.

---

## 🏦 Topic 3: Deadlock Avoidance: Banker’s Algorithm

### **Introduction: Planning Ahead** 🔮

**Deadlock Avoidance** is a dynamic approach. The OS grants a resource request only if doing so leaves the system in a **Safe State**. It requires prior information about the maximum resource needs of each process.

* **Safe State:** A system is in a safe state if there exists a **safe sequence** of processes.
* **Safe Sequence:** A sequence of processes $\langle P_1, P_2, \dots, P_n \rangle$ such that for each $P_i$, the resources $P_i$ might still request can be satisfied by the currently available resources **plus** the resources held by all $P_j$ where $j < i$.

### **The Banker’s Algorithm** 💰

* **Analogy:** A banker who only lends money to clients (processes) if they can prove that, even under the worst-case scenario (all other clients maximize their borrowing), the bank (OS) can still meet every client's maximum need and guarantee repayment.
* **Key Data Structures (The Banker's Books):**
    1.  **Available:** A vector showing the number of available instances of each resource type.
    2.  **Max:** A matrix showing the maximum number of instances of each resource type that each process may ever request.
    3.  **Allocation:** A matrix showing the number of resources of each type currently allocated to each process.
    4.  **Need:** A matrix showing the remaining resources each process needs: $\text{Need} = \text{Max} - \text{Allocation}$.

#### **1. Safety Algorithm (Finding a Safe Sequence)**
This algorithm checks if the current state is safe.

1.  Let $\text{Work} = \text{Available}$.
2.  Let $\text{Finish}[i] = \text{false}$ for all processes $i$.
3.  Find a process $P_i$ such that $\text{Finish}[i] = \text{false}$ and $\text{Need}[i] \le \text{Work}$.
4.  If such a $P_i$ is found, assume it executes and releases its resources: $\text{Work} = \text{Work} + \text{Allocation}[i]$. Set $\text{Finish}[i] = \text{true}$.
5.  Repeat Step 3 until all processes are marked $\text{Finish}[i] = \text{true}$.
6.  If all processes are finished, the system is in a **Safe State**, and the sequence of processes found is a safe sequence.

#### **2. Resource-Request Algorithm (Deciding to Grant Request)**
When a process $P_i$ requests resources (Request):

1.  Check: If $\text{Request} \le \text{Need}[i]$. If not, the request is invalid.
2.  Check: If $\text{Request} \le \text{Available}$. If not, $P_i$ must wait (not enough resources).
3.  **Pretend to allocate:** Temporarily modify the system state:
    * $\text{Available} = \text{Available} - \text{Request}$
    * $\text{Allocation}[i] = \text{Allocation}[i] + \text{Request}$
    * $\text{Need}[i] = \text{Need}[i] - \text{Request}$
4.  **Check Safety:** Run the **Safety Algorithm** on the new, hypothetical state.
5.  If the new state is **Safe**, the request is **granted**. If the new state is **Unsafe**, the allocation is undone, and $P_i$ must wait.

### **Important Keywords** 📌

* **Safe State:** Guarantees a non-deadlocked future.
* **Unsafe State:** A state where deadlock **might** occur (but not guaranteed).
* **Prior Knowledge:** Deadlock Avoidance requires knowing the $\text{Max}$ resource needs of every process beforehand.

---

## 🔎 Topic 4: Deadlock Detection and Recovery

### **Introduction: Cleaning Up the Mess** 🗑️

If you don't use prevention or avoidance schemes, deadlocks may occur. **Deadlock Detection** is the process of periodically checking the system state (the RAG) to determine if a deadlock exists. **Recovery** is the process of breaking the detected deadlock.

### **Deadlock Detection** 🧐

* **Concept:** It uses an algorithm similar to the Banker's Safety Algorithm to check the RAG for cycles. If a cycle exists and all involved resources are held by waiting processes, a deadlock is present.
* **When to Run Detection:**
    1.  **Every time a request is made:** High overhead, but immediate detection.
    2.  **Periodically:** (e.g., every hour or when CPU utilization drops below 40%). Less overhead, but deadlocks can persist for some time.
* **Detection Algorithm (Resource-Type with Multiple Instances):**
    * Uses the same $\text{Work}$, $\text{Allocation}$, and $\text{Request}$ matrices/vectors as the Banker's algorithm.
    * The system is deadlocked if and only if there is a subset of processes that are **not** in the $\text{Finish}$ set (i.e., they are blocked and waiting forever).

### **Deadlock Recovery** 🚑

Once a deadlock is detected, the OS must recover. Recovery methods involve breaking the circular wait condition.

#### **1. Process Termination (The Brutal Method)** 🔪
* **Concept:** Abort one or more deadlocked processes to break the cycle.
* **Methods:**
    * **Aborting All Deadlocked Processes:** Simplest method, but the costliest.
    * **Aborting One Process at a Time:** Run the detection algorithm after each abortion until the deadlock cycle is broken.
* **Selection Criteria (Which process to abort?):**
    * Least time consumed so far.
    * Least number of resources held.
    * Process priority (abort the lowest priority process).

#### **2. Resource Pre-emption (The Rollback Method)** 🔙
* **Concept:** Forcibly take a resource from a deadlocked process and give it to another process, thereby breaking the circular wait.
* **Steps:**
    1.  **Select a Victim:** Choose a resource to pre-empt from a process. (Often involves minimizing rollback cost).
    2.  **Rollback:** The victim process must be rolled back to some prior **safe state** and restarted from that state. This is to ensure the process's work remains consistent.
    3.  **Starvation:** Ensure that the same process is not always chosen as the victim (implement a cost factor to prevent this).

### **Summary or Revision Points** 💡

| Strategy | Goal | Resource Utilization | Overhead/Cost |
| :--- | :--- | :--- | :--- |
| **Prevention** | Ensure one condition **never** holds. | Low (wastes resources). | High (pre-allocation, strict ordering). |
| **Avoidance** | Grant resource only if it maintains a **Safe State**. | High (efficient). | High (requires prior knowledge, complex algorithm). |
| **Detection** | Allow deadlocks, **identify** and **recover** later. | High (no restrictions). | Medium (periodic checking and recovery/rollback cost). |