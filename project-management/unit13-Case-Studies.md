


# 💻 Module 13: Case Studies and MS-Project Application

### 📌 Introduction
Case studies in project management test your ability to apply planning, scheduling, and control concepts (Modules 10-12) to a real-world scenario. Your solution must demonstrate a systematic, step-by-step methodology using tools like the **Work Breakdown Structure (WBS)** and **Critical Path Method (CPM)**, which are easily executed in MS Project.



## 1. Case Study Framework: 5 Steps to Solution

To effectively solve a project management case study (e.g., "Schedule a product launch project"), follow this structured process:

| Step | Focus | Key Deliverable in MS Project / Report |
| :--- | :--- | :--- |
| **1. Define & Scope** | Clarify the objectives, final deliverables, and constraints (Scope, Time, Cost). | **Project Start/Finish Dates**, **Scope Statement** (as understood from the case). |
| **2. Decompose (WBS)** | Break the project down into manageable, definable tasks. | **Hierarchical Task List** (WBS output). |
| **3. Sequence & Schedule** | Determine task dependencies, duration estimates, and resource assignments. | **Network Diagram Logic** (Predecessors), **Gantt Chart** with task durations. |
| **4. Calculate & Analyze** | Determine the shortest project duration and identify time buffers. | **Critical Path**, **Total Float/Slack** for all tasks. |
| **5. Control & Recommend** | Propose actions for recovery (if behind schedule) or optimization (if over budget). | **Crashing Plan**, **Time-Cost Trade-off** Analysis, **EVM** metrics. |

---

## 2. Key MS Project Concepts and Application

MS Project automates the complex calculations involved in scheduling. Your report must reference how these core functions are used to manage the triple constraint.

### A. Scheduling and Time Management
* **Task Entry and WBS:** Tasks are entered sequentially and grouped using **Summary Tasks** and **Sub-tasks**. MS Project automatically generates WBS codes (Level 1, 1.1, 1.1.1).
* **Dependencies (Sequencing):** Tasks are linked using **predecessor** and **successor** relationships (e.g., Finish-to-Start, FS). This linkage is the basis of the CPM calculation.
* **Critical Path Identification:** MS Project calculates the **Earliest Start (ES)** and **Latest Finish (LF)** dates for every task. The tasks with **Total Slack** of zero (or the minimum non-zero value) are highlighted as the **Critical Path**.

### B. Resource Management and Costing
* **Resource Sheet:** Define all resources (Work, Material, Cost) and their costs (Standard Rate, Overtime Rate, Cost per Use).
* **Assignment:** Resources are assigned to specific tasks, and MS Project calculates the **Total Budget** based on the resources' duration and rates.
* **Resource Leveling:** When a resource is **over-allocated** (assigned to more work than they can handle at once), the software can automatically delay or shift non-critical tasks to resolve the conflict without delaying the project finish date.

### C. Monitoring and Control (Baseline and Tracking)
* **Setting the Baseline:** Once the plan is approved, the PM sets the **Baseline**. This saves the original planned schedule, cost, and duration for comparison.
* **Tracking Progress:** During execution, the PM tracks the **% Complete** for each task. MS Project compares the actual progress against the baseline, generating variances.
* **Earned Value Management (EVM):** MS Project can calculate core EVM metrics:
    * **$\text{CV}$ (Cost Variance):** $\text{EV} - \text{AC}$ (Are we over or under budget?)
    * **$\text{SV}$ (Schedule Variance):** $\text{EV} - \text{PV}$ (Are we ahead or behind schedule?)

---

## 3. Advanced Case Study Topics

Case studies often move beyond simple scheduling and test your ability to apply corrective action.

### A. Time-Cost Trade-off and Crashing
If a case study requires shortening the schedule (crashing), your analysis should follow the steps below:
1.  **Identify Critical Tasks:** Use MS Project to filter tasks with zero slack.
2.  **Calculate Crash Cost:** Determine the **Crash Cost per Unit Time** (as per Module 11) for each critical task.
3.  **Apply Crashing:** Shorten the critical task with the **lowest cost per unit time** until the desired duration is met or a **new critical path** emerges.
4.  **Evaluate:** Demonstrate the new shorter duration and the **total additional cost** incurred.

### B. Handling Scope Creep
If the case introduces new requirements after the baseline is set (scope creep), your solution should detail the **Integrated Change Control** process:
1.  **Document:** Log the change request, describing the new scope and its impact.
2.  **Analyze:** Estimate the **new cost, duration, and resource needs** in MS Project.
3.  **Decision:** Recommend approval or rejection to the Change Control Board (CCB).
4.  **Update Baseline:** If approved, update the baseline in MS Project to reflect the approved changes.

---

## 4. Report Structure for a Case Study Exam Answer

Your written solution should be structured like a formal mini-Project Management Plan:

### I. Executive Summary
* State the problem and the final project duration/cost achieved.

### II. Planning Output (WBS and Schedule)
* Include the WBS structure (Level 1, 2, 3) used.
* Present the **Gantt Chart** (conceptual sketch or table) showing Task ID, Name, Duration, and Predecessors.

### III. Critical Path Analysis (The Calculation)
* **Identify the Critical Path:** List the sequence of tasks that determine the project length.
* **Calculate Total Float:** Explicitly state the total float available for a few non-critical tasks.
* **Conclusion:** State the minimum achievable project duration.

### IV. Corrective Action and Recommendation (The Analysis)
* If the case requires **crashing**, present the **Crash Cost/Time** calculation and the resulting cost increase.
* If the case involves **EVM**, calculate $\text{SPI}$ and $\text{CPI}$ and explain the status (e.g., "Since $\text{SPI} = 0.85$, the project is 15% behind schedule, requiring corrective action...").

---

### ❤️ **Made with love and caffeine ☕**
<div align="right" style="font-size:20px;">
  <strong><span style="color:green;">--- agontuk</span></strong>
</div>