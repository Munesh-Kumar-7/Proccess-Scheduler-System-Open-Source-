# Process Scheduling

A C++ implementation of various CPU scheduling algorithms used in operating systems. This project demonstrates how different scheduling techniques manage process execution, allocate CPU time, and handle process priorities.

The implemented algorithms include First Come First Serve (FCFS), Round Robin (RR), Shortest Process Next (SPN), Shortest Remaining Time (SRT), Highest Response Ratio Next (HRRN), Feedback (FB), Feedback with Variable Quantum (FBV), and Aging.

## Table of Contents

- [Process Scheduling](#process-scheduling)
- [Scheduling Algorithms](#scheduling-algorithms)
- [First Come First Serve (FCFS)](#1-first-come-first-serve-fcfs)
- [Round Robin (RR)](#2-round-robin-rr)
- [Shortest Process Next (SPN)](#3-shortest-process-next-spn)
- [Shortest Remaining Time (SRT)](#4-shortest-remaining-time-srt)
- [Highest Response Ratio Next (HRRN)](#5-highest-response-ratio-next-hrrn)
- [Feedback (FB)](#6-feedback-fb)
- [Feedback with Variable Quantum (FBV)](#7-feedback-with-variable-quantum-fbv)
- [Aging](#8-aging)
- [Installation](#installation)
- [Input Format](#input-format)
- [Contributors](#contributors)

## Scheduling Algorithms

### 1. First Come First Serve (FCFS)

First Come First Serve is a non-preemptive scheduling algorithm that executes processes according to their arrival order. The process that enters the ready queue first is assigned the CPU first.

It is simple to understand and implement. However, longer processes can delay shorter ones, resulting in increased average waiting time. This limitation is commonly known as the convoy effect.

### 2. Round Robin (RR)

Round Robin is a preemptive scheduling algorithm commonly used in time-sharing systems. It assigns each process a fixed amount of CPU time, known as a time quantum.

Processes are maintained in a ready queue and executed sequentially. If a process cannot complete within its allocated time quantum, it is interrupted and moved to the end of the queue.

This implementation supports varying time quantum values, allowing flexibility in CPU time allocation while providing each process with an opportunity to execute.

### 3. Shortest Process Next (SPN)

Shortest Process Next is a non-preemptive scheduling algorithm that selects the process with the smallest CPU burst time from the ready queue.

Whenever the CPU becomes available, the scheduler examines the available processes and chooses the one requiring the least execution time. Once selected, the process continues until completion.

SPN can reduce average waiting time by prioritizing shorter processes. However, longer processes may experience starvation if shorter processes continuously arrive.

### 4. Shortest Remaining Time (SRT)

Shortest Remaining Time is the preemptive version of Shortest Process Next.

The scheduler selects the process with the smallest remaining execution time. If a new process arrives with a shorter burst time than the remaining time of the currently executing process, the current process can be interrupted.

This approach can improve average waiting and turnaround times. However, frequent context switching and potential starvation of longer processes are its limitations.

### 5. Highest Response Ratio Next (HRRN)

Highest Response Ratio Next is a non-preemptive scheduling algorithm that considers both the waiting time and service time of processes.

The scheduler calculates the response ratio of each process in the ready queue and selects the process with the highest value.

The response ratio is calculated using:

**Response Ratio = (Waiting Time + Burst Time) / Burst Time**

HRRN balances the preference for shorter processes with the need to prevent longer processes from waiting indefinitely. As a process waits longer, its response ratio increases, improving its chances of being selected.

### 6. Feedback (FB)

Feedback scheduling is a multi-level priority scheduling algorithm that uses multiple ready queues to manage processes according to their priority levels.

Processes are assigned to different queues, and the scheduler gives preference to processes in higher-priority queues.

As processes execute, their priority levels may change according to the feedback scheduling policy. This approach helps manage both short-running and long-running processes.

### 7. Feedback with Variable Quantum (FBV)

Feedback with Variable Quantum follows the same general approach as Feedback scheduling but assigns different time quantum values to different priority levels.

Each queue has its own time quantum, allowing the scheduler to allocate CPU time according to the queue level.

This technique combines multi-level feedback queues with variable execution time slices.

### 8. Aging

Aging is a scheduling technique designed to prevent starvation in priority-based scheduling systems.

In priority scheduling, lower-priority processes may remain in the ready queue for extended periods because higher-priority processes continuously receive CPU time.

Aging solves this problem by gradually increasing the priority of waiting processes whenever the scheduler is invoked.

The scheduling procedure follows these steps:

1. Restore the priority of the currently running process to its original priority.
2. Increase the priority of every process waiting in the ready queue by a fixed amount.
3. Select the eligible process with the highest priority for execution.

By gradually increasing the priority of waiting processes, Aging ensures that they eventually receive an opportunity to execute.

This implementation follows the aging-based scheduling approach used in the Xinu operating system.

## Installation

Follow these steps to download, compile, and execute the project.

**1. Clone the repository**

```bash
git clone <repository-url>
```

**2. Install the required compiler and build tools**

For Ubuntu or Debian-based Linux distributions:

```bash
sudo apt-get update
sudo apt-get install g++ make
```

**3. Compile the project**

Navigate to the project directory and execute:

```bash
make
```

**4. Run the executable**

```bash
./<executable-name>
```

## Input Format

The program accepts input through standard input. The input consists of the following sections:

**Line 1: Execution Mode**

Specify one of the following modes:

- `trace` – Displays the execution timeline of the selected scheduling algorithms.
- `stats` – Displays scheduling statistics for the selected algorithms.

**Line 2: Scheduling Policies**

Provide a comma-separated list of scheduling algorithms along with their parameters, where required.

The supported scheduling policies are:

| Number | Algorithm |
|---|---|
| 1 | FCFS |
| 2 | Round Robin (RR) |
| 3 | Shortest Process Next (SPN) |
| 4 | Shortest Remaining Time (SRT) |
| 5 | Highest Response Ratio Next (HRRN) |
| 6 | Feedback (FB-1) |
| 7 | Feedback with Variable Quantum (FB-2i) |
| 8 | Aging |

Round Robin and Aging require a parameter specifying the time quantum or scheduling increment.

Examples:

- `2-4` represents Round Robin with a time quantum of 4.
- `8-1` represents Aging with a parameter value of 1.

**Line 3: Simulation Limit**

An integer specifying the final time instant to be included in the simulation and displayed in the execution timeline.

**Line 4: Number of Processes**

An integer representing the total number of processes in the simulation.

**Line 5 Onwards: Process Information**

Each process must be described on a separate line.

For scheduling algorithms 1 through 7, provide the following comma-separated information:

1. Process name (string).
2. Arrival time.
3. Service time (CPU burst time).

For the Aging algorithm (algorithm 8), provide:

1. Process name (string).
2. Arrival time.
3. Initial priority.

### Input Assumptions

- Processes are provided in ascending order of their arrival times.
- If multiple processes have the same arrival time, the process with the lower priority is considered to arrive first.
- Each process must follow the input structure required by its selected scheduling algorithm.

Refer to the provided test cases for additional input examples and expected output formats.

## Contributors

- Munesh
- Anesh
- Parshant
