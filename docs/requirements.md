RTOScope Requirements Specification

Project: RTOScope
Subtitle: Interactive Real-Time Operating System Monitor & Scheduler
Version: 0.1.0
Date: September 4, 2026
Status: Draft

⸻

1. Project Overview

RTOScope is an embedded systems project designed to demonstrate and visualize operating system concepts using an ESP32 microcontroller and a real-time operating system (RTOS).

The system will provide an interactive user interface through which users can observe and interact with tasks, scheduling, inter-task communication, synchronization mechanisms, interrupts, and system resources.

The project will use FreeRTOS as the underlying RTOS while implementing additional software components to visualize, analyze, and demonstrate operating system behavior.

⸻

2. Project Goals

The primary goals of RTOScope are to:

1. Demonstrate fundamental operating system concepts on a physical embedded platform.
2. Provide a visual representation of real-time task execution and scheduling.
3. Demonstrate communication and synchronization between concurrent tasks.
4. Demonstrate interaction between hardware events and operating system tasks.
5. Measure and display system resource usage and performance.
6. Provide an interactive interface for controlling and observing the system.
7. Develop a project using professional software engineering practices, including version control, documentation, testing, and structured development.

⸻

3. Functional Requirements

3.1 Task Management

FR-001 — Task Monitoring
The system shall display information about active RTOS tasks.

FR-002 — Task State Monitoring
The system shall display the current state of monitored tasks, including states such as running, ready, blocked, or suspended where supported by the underlying RTOS.

FR-003 — Task Priority Monitoring
The system shall display the priority assigned to each monitored task.

FR-004 — Task Control
The system shall provide a mechanism for the user to suspend and resume selected tasks.

FR-005 — Task Creation and Removal
The system should provide a mechanism for creating and removing demonstration tasks where technically appropriate.

⸻

3.2 Scheduling

FR-006 — Scheduler Monitoring
The system shall provide a visualization of task scheduling activity.

FR-007 — Scheduling Algorithms
The project shall implement and demonstrate multiple scheduling algorithms in a software simulation.

The initial algorithms shall include:

* First-Come, First-Served (FCFS)
* Round Robin
* Priority Scheduling
* Non-preemptive Scheduling

FR-008 — Scheduling Metrics
The scheduler simulation shall calculate relevant scheduling metrics, including:

* Waiting time
* Turnaround time
* Response time
* Completion time
* Number of context switches where applicable

FR-009 — Scheduling Comparison
The system should provide a method for comparing the performance of different scheduling algorithms.

FR-010 — RTOS Scheduling Demonstration
The embedded system shall demonstrate actual task scheduling behavior using FreeRTOS.

⸻

3.3 Inter-Task Communication

FR-011 — Inter-Task Communication
The system shall demonstrate communication between concurrent tasks.

FR-012 — Queue Demonstration
The system shall use an RTOS-supported queue or equivalent message-passing mechanism to demonstrate inter-task communication.

FR-013 — IPC Monitoring
The user interface should display relevant information about messages being passed between demonstration tasks.

⸻

3.4 Synchronization

FR-014 — Resource Synchronization
The system shall demonstrate synchronization between concurrent tasks.

FR-015 — Mutex Demonstration
The system should demonstrate the use of a mutex to protect access to a shared resource.

FR-016 — Semaphore Demonstration
The system should demonstrate the use of a semaphore or equivalent synchronization mechanism.

FR-017 — Synchronization Monitoring
The user interface should display the state of selected synchronization mechanisms and the tasks interacting with them.

⸻

3.5 Interrupt Handling

FR-018 — Hardware Interrupt
The system shall respond to at least one physical hardware event using an interrupt mechanism.

FR-019 — Interrupt-to-Task Communication
The system shall demonstrate communication between a hardware interrupt and an RTOS task.

⸻

3.6 Hardware Interface

FR-020 — Microcontroller Interface
The system shall operate on an ESP32 microcontroller.

FR-021 — User Interface Hardware
The system shall provide a physical display capable of presenting system information and receiving user input.

FR-022 — Physical Input
The system shall incorporate at least one physical input device or sensor in addition to the primary user interface.

FR-023 — Physical Output
The system shall incorporate at least one physical output device, such as an LED, buzzer, or other actuator.

FR-024 — Hardware/Software Integration
The system shall demonstrate interaction between physical hardware and software tasks running under the RTOS.

⸻

3.7 System Monitoring

FR-025 — System Resource Monitoring
The system shall display available system resource information where supported by the ESP32 and RTOS.

Potential metrics include:

* Available heap memory
* Task count
* Task runtime
* CPU utilization
* System uptime

FR-026 — Real-Time Updates
System monitoring information shall update periodically while the RTOS is running.

⸻

3.8 User Interface

FR-027 — Main Interface
The system shall provide a primary interface through which the user can access the project’s demonstrations.

FR-028 — Task Interface
The interface shall provide a screen for viewing task information.

FR-029 — Scheduler Interface
The interface shall provide a screen for viewing scheduling information.

FR-030 — IPC Interface
The interface should provide a screen for viewing inter-task communication.

FR-031 — Synchronization Interface
The interface should provide a screen for viewing synchronization demonstrations.

FR-032 — System Monitor Interface
The interface shall provide a screen for viewing system resource information.

⸻

4. Non-Functional Requirements

4.1 Performance

NFR-001 — Responsiveness
The user interface should remain responsive while background RTOS tasks are executing.

NFR-002 — Real-Time Operation
Demonstration tasks shall execute according to their configured timing and scheduling behavior.

NFR-003 — Measurement
Where practical, system behavior shall be measured rather than relying solely on qualitative observations.

⸻

4.2 Reliability

NFR-004 — Stability
The system should continue operating without unintended crashes during normal demonstration conditions.

NFR-005 — Error Handling
The software should detect and handle foreseeable errors where practical.

⸻

4.3 Maintainability

NFR-006 — Modular Design
The software shall be organized into logical components with clearly defined responsibilities.

NFR-007 — Documentation
Major software components shall contain appropriate documentation explaining their purpose and operation.

NFR-008 — Version Control
Source code and project documentation shall be maintained using Git version control.

⸻

4.4 Testing

NFR-009 — Component Testing
Individual software components shall be tested independently where practical.

NFR-010 — Integration Testing
Integrated hardware and software functionality shall be tested before the final demonstration.

NFR-011 — Test Documentation
Test procedures and results shall be documented.

⸻

4.5 Documentation

NFR-012 — Development History
Development progress, including successful and unsuccessful attempts, shall be documented throughout the project.

NFR-013 — Technical Documentation
The final project shall include documentation describing the system architecture, hardware, software, interfaces, testing, and results.

⸻

5. Stretch Goals

The following features are considered optional and shall only be implemented if the core requirements can be completed successfully.

SG-001 — Additional Scheduling Algorithms
Implement additional scheduling algorithms beyond the required algorithms.

SG-002 — Priority Inversion Demonstration
Demonstrate and visualize priority inversion and the behavior of an appropriate mitigation mechanism.

SG-003 — Scheduling Timeline
Provide a graphical timeline showing task execution over time.

SG-004 — Historical Performance Graphs
Display historical CPU utilization, memory usage, or scheduling information.

SG-005 — Additional IPC Mechanisms
Demonstrate additional FreeRTOS communication mechanisms.

SG-006 — Advanced Hardware Demonstration
Add additional sensors, actuators, or peripherals that provide meaningful operating system demonstrations.

SG-007 — System Logging
Provide persistent or exportable system logs for later performance analysis.

⸻

6. Project Constraints

The project shall:

* Use an ESP32 microcontroller as the primary embedded platform.
* Use FreeRTOS as the underlying real-time operating system.
* Include both hardware and software components.
* Provide a functional user interface.
* Demonstrate multiple operating system concepts.
* Be sufficiently complex to satisfy the project’s hardware and software complexity requirements.

Specific hardware components and implementation details will be finalized during the design phase.

⸻

7. Requirement Status

Requirements will be tracked throughout development using the following statuses:

Status	Meaning
Planned	Requirement has been identified but work has not started.
In Progress	Implementation or investigation is underway.
Complete	Requirement has been implemented and verified.
Blocked	Work cannot continue because of an unresolved dependency or problem.
Deferred	Requirement has been intentionally postponed.
Cancelled	Requirement has been removed from the project scope.

⸻

8. Revision History

Version	Date	Description
0.1.0	September 4, 2026	Initial requirements specification.

⸻

9. Notes

This document represents the initial requirements baseline for RTOScope. Requirements may be revised as hardware capabilities, technical limitations, testing results, and project scope are better understood. Significant changes shall be recorded in the project’s development log and revision history.