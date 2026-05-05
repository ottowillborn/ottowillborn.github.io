+++
title = "Deadline Driven Scheduler"
date = "2026-02-01"
description = "FreeRTOS custom deadline-driven scheduler"
repo = "https://github.com/ottowillborn/FreeRTOS_DDS"
stack = ["c", "embedded systems"]
featured = true
+++

## Deadline-Driven Scheduler (DDS) System

Built a comprehensive real-time scheduling system for STM32 microcontrollers using FreeRTOS. The project involved implementing an Earliest Deadline First (EDF) scheduling algorithm to dynamically manage, preempt, and monitor periodic, time-sensitive tasks.

---

### Technical Highlights
* **Real-Time Scheduling:** Implemented a preemptive EDF scheduler to ensure tasks with the most urgent absolute deadlines receive CPU priority.
* **Inter-Task Communication:** Engineered a robust IPC architecture using FreeRTOS queues to handle synchronization between task generators, the scheduler, and monitor components.
* **Memory & Resource Management:** Managed dynamic task creation/deletion, preventing memory leaks through rigorous cleanup of task handles within the scheduler loop.
* **Preemption Logic:** Designed a priority-manipulation mechanism that allows the scheduler to preempt running tasks mid-execution, recording remaining runtime for resumption.
* **System Profiling:** Analyzed system performance under varying workloads, identifying the impact of processing jitters on scheduling accuracy and the necessity of "slack time" in real-time systems.

---

### Implementation Details
The system architecture was modular, separating generation, scheduling, and monitoring into distinct, high-performance components:

* **DDSchedulerTask:** The system core. It acts as an API, processing messages (e.g., `MSG_RELEASE`, `MSG_COMPLETE`) and maintaining the task list as a sorted, singly-linked list to facilitate constant-time priority lookups.
* **DDGeneratorTask:** Functions as the factory, periodically generating workloads, assigning absolute deadlines, and interfacing with the scheduler.
* **DDSMonitorTask:** Handles system reporting without interfering with the scheduler’s real-time operations, utilizing queue snapshots to display active, completed, and overdue task counts.
* **User-Defined Tasks:** Acted as workload simulators, consuming CPU cycles and comparing elapsed time against target times to simulate realistic embedded behavior.

---

### Key Learnings
* **Embedded Design:** Gained experience in designing modular components that operate under strict memory and timing constraints.
* **Jitter Analysis:** Developed an appreciation for real-world limitations in embedded systems; identified how OS overhead and print statements can introduce latency (jitter) and affect deadline compliance.
* **Data Structures:** Successfully implemented a custom linked list for the scheduler, refining sorting logic to handle complex scenarios, including tie-breakers based on remaining execution time.

### Gallery
{{< gallery >}}
![Alt text](/images/sysdiag.png)
{{< /gallery >}}