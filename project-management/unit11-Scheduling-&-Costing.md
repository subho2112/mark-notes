


# ⏰ Module 11: Project Scheduling and Costing Study Notes



## 1. Project Scheduling Tools: Gantt Chart, CPM, and PERT

### 📌 Introduction
Project scheduling is the process of determining when project activities will take place. The primary tools used—**Gantt Charts, CPM, and PERT**—provide visual representation, time control, and risk analysis for the project timeline.

### 💡 Core Scheduling Tools

| Tool | Focus/Purpose | Structure | Key Benefit |
| :--- | :--- | :--- | :--- |
| **Gantt Chart** | **Visualization & Tracking** | A horizontal bar chart illustrating the start and end dates of terminal elements of a project. | **Simple to read** and excellent for tracking progress against the schedule **baseline**. |
| **CPM** (Critical Path Method) | **Deterministic Time Control** | A network diagram using **single-point time estimates** to determine the longest path of dependent activities. | Identifies the **Critical Path** and the **minimum time** required to complete the project. |
| **PERT** (Program Evaluation and Review Technique) | **Probabilistic Time Control** | A network diagram using **three time estimates** (Optimistic, Pessimistic, Most Likely) to calculate the expected duration. | Used for **high-uncertainty** projects (R&D) to estimate duration with an associated probability. |

#### PERT Expected Time Calculation
For PERT analysis, the estimated duration of an activity ($T_e$) is calculated using a beta probability distribution:

$$T_e = \frac{T_o + 4T_m + T_p}{6}$$

Where:
* $T_o$ = Optimistic Time (best case)
* $T_m$ = Most Likely Time
* $T_p$ = Pessimistic Time (worst case)

### 🔑 Important Keywords
**Gantt Chart**, **CPM**, **PERT**, **Deterministic**, **Probabilistic**, **$T_e$ (Expected Time)**.

### ✅ Summary/Revision Points
* **Gantt** is for **visualization** and communicating status.
* **CPM** is for **precise scheduling** with known durations.
* **PERT** is for **uncertain projects** using weighted average estimates.

---

## 2. Critical Path and Floats (Slacks)

### 📌 Introduction
The **Critical Path** is the most crucial concept in network scheduling (CPM/PERT). It governs the project's overall duration, while **Floats** (or Slacks) identify where flexibility exists.

### 💡 The Critical Path
* **Definition:** The longest sequence of dependent activities in the project network diagram. It determines the shortest possible duration in which the project can be completed.
* **Significance:**
    1.  **Time Management:** Any delay to an activity on the critical path will directly delay the **entire project completion date**.
    2.  **Focus Area:** The Project Manager must monitor and control critical path activities most rigorously, dedicating extra resources here if needed.
    3.  **Zero Slack:** Critical activities have **zero float (slack)**.

### 💡 Floats (Slacks)
**Float** (or **Slack**) is the amount of time an activity can be delayed without affecting the overall project schedule or the start of other activities.

| Type of Float | Definition | Formula | Significance |
| :--- | :--- | :--- | :--- |
| **Total Float (TF)** | The amount of time an activity can be delayed without delaying the **project completion date**. | $TF = LS - ES$ or $LF - EF$ | Indicates scheduling flexibility for non-critical activities. $|TF = 0|$ for critical path activities. |
| **Free Float (FF)** | The amount of time an activity can be delayed without delaying the **Early Start (ES)** of its immediate successor activity. | $FF = \min(ES \text{ of successor}) - EF$ | Indicates local flexibility that doesn't impact any other activity in the network. |

* **Earliest Start (ES) / Earliest Finish (EF):** The earliest an activity can start/finish based on preceding activities.
* **Latest Start (LS) / Latest Finish (LF):** The latest an activity can start/finish without delaying the project finish date.

### 🔑 Important Keywords
**Critical Path**, **Total Float**, **Free Float**, **Zero Slack**, **Successor Activity**.

### ✅ Summary/Revision Points
* The **Critical Path** is the sequence of tasks with the **longest duration** and **zero float**.
* **Total Float** indicates how much time a task can slip before the **project finish** date slips.
* **Float** is a PM's buffer for managing resource leveling and unexpected issues on non-critical tasks.

---

## 3. Crashing, Time-Cost Trade-off Analysis, and Cost Reduction

### 📌 Introduction
During execution, projects often face pressure to finish early or within a reduced budget. **Crashing** and **Time-Cost Trade-off Analysis** are techniques used to systematically manage this pressure.

### 💡 Crashing and Time-Cost Trade-off Analysis
* **Crashing:** A schedule compression technique used to shorten the project duration by adding resources to specific activities.
* **Principle of Crashing:** Crash only **critical path activities**. Crashing non-critical tasks is wasteful, as they won't shorten the project duration.
* **Time-Cost Trade-off Analysis:** The systematic process of comparing the cost of accelerating activities (crashing) against the financial benefits (e.g., avoiding penalties, realizing early revenue).

#### Key Calculation: Crash Cost per Unit Time
To decide which critical activity to crash, the PM must calculate the cost of speeding up each activity by one unit of time (day/week).

$$\text{Crash Cost/Unit Time} = \frac{\text{Crash Cost} - \text{Normal Cost}}{\text{Normal Time} - \text{Crash Time}}$$

* **Decision Rule:** The PM should prioritize crashing the critical activity with the **lowest Crash Cost per Unit Time** until the desired duration is reached, or until the crashing activity creates a *new critical path*.

### 💡 Project Cost Reduction Methods
Instead of increasing cost (crashing), projects often seek to reduce costs without compromising scope or quality.

1.  **Value Engineering/Analysis (VE/VA):** Systematic review of the product design or process to achieve the necessary function at the lowest life-cycle cost without sacrificing essential performance or reliability.
    * *Example:* Changing a component material from an expensive alloy to a cheaper composite that still meets all performance specs.
2.  **Optimized Procurement/Negotiation:** Bulk purchasing discounts, leveraging favorable market timing for material acquisition, or negotiating better terms with vendors (e.g., just-in-time delivery).
3.  **Resource Leveling/Optimization:** Assigning resources efficiently to smooth out peak demand and reduce the need for expensive overtime or short-term rentals. Utilizing internal resources before expensive external contractors.
4.  **Improved Process Efficiency (Kaizen):** Implementing quality management techniques (e.g., Six Sigma, Lean) to minimize waste, rework, and defects, which are significant project costs.

### 🔑 Important Keywords
**Crashing**, **Schedule Compression**, **Time-Cost Trade-off**, **Crash Cost/Unit Time**, **Value Engineering (VE)**, **Resource Leveling**.

### ✅ Summary/Revision Points
* **Crashing** shortens the schedule but **increases cost**, and must only be applied to **critical path activities**.
* **Time-Cost Trade-off** uses the **Crash Cost per Unit Time** to select the most cost-effective activity for acceleration.

* **Cost Reduction** focuses on techniques like **Value Engineering** and **process optimization** to lower the baseline budget.
