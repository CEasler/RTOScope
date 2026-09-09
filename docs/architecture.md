RTOScope System Architecture

Project: RTOScope
Subtitle: Interactive Real-Time Operating System Monitor & Scheduler
Version: 0.1.0
Date: September 4, 2026
Status: Draft

⸻

1. Purpose

This document defines the initial software and hardware architecture of RTOScope.

The architecture is designed to separate the user interface, operating system demonstrations, system monitoring, scheduling analysis, and hardware interfaces into independent components. This modular structure is intended to simplify development, testing, debugging, and future expansion.

The architecture will be refined throughout development as hardware capabilities and implementation details are established.

⸻

2. System Overview

RTOScope will be an embedded operating system monitoring and demonstration platform built around an ESP32 microcontroller.

FreeRTOS will provide the underlying real-time operating system functionality, including task management, scheduling, inter-task communication, synchronization primitives, and timing mechanisms.

RTOScope will provide an application layer that exposes selected operating system concepts through an interactive user interface.

The system will also include a host-based scheduler simulator. The simulator will allow scheduling algorithms to be developed and tested independently from the embedded hardware.

High-Level Architecture

                         USER
                           │
                           ▼
                ┌─────────────────────┐
                │   Touchscreen UI    │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    RTOScope Core    │
                └──────────┬──────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
┌───────────────┐  ┌───────────────┐  ┌────────────────┐
│ Task Manager  │  │   Scheduler   │  │ System Monitor │
└───────────────┘  └───────────────┘  └────────────────┘
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  FreeRTOS   │
                    └──────┬──────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
          Tasks          Queues       Mutexes/
                                      Semaphores
             │
             ▼
          ESP32
             │
      ┌──────┼──────────────┐
      │      │              │
      ▼      ▼              ▼
   Display  Sensors       LEDs/
             │            Outputs
             │
             ▼
         Hardware
         Interrupts

⸻

3. Architectural Principles

RTOScope will follow the following design principles.

3.1 Modularity

Major system functions shall be separated into independent software modules.

A change to one subsystem should require minimal changes to unrelated subsystems.

3.2 Separation of Concerns

The user interface should not directly control low-level hardware or RTOS functionality where avoidable.

Instead, communication should occur through defined interfaces between system components.

3.3 Hardware Abstraction

Hardware-specific functionality should be isolated from the primary application logic where practical.

This will allow hardware components to be replaced or modified without requiring major changes to the rest of the system.

3.4 Measurability

System behavior should be observable through measurable metrics rather than relying solely on visual demonstrations.

Examples include:

* Task execution time
* CPU utilization
* Memory utilization
* Scheduling latency
* Waiting time
* Turnaround time
* Response time
* Context-switch activity

3.5 Incremental Development

The project will be developed in stages.

Each major subsystem should be tested independently before being integrated into the complete system.

⸻

4. Software Architecture

RTOScope software will be divided into several logical layers.

┌─────────────────────────────────────────┐
│              User Interface             │
├─────────────────────────────────────────┤
│             RTOScope Core                │
├──────────────┬──────────────┬───────────┤
│ Task Manager │ Scheduler    │ Monitoring│
├──────────────┴──────────────┴───────────┤
│        IPC / Synchronization Layer      │
├─────────────────────────────────────────┤
│                FreeRTOS                  │
├─────────────────────────────────────────┤
│             Hardware Layer              │
├─────────────────────────────────────────┤
│                ESP32                    │
└─────────────────────────────────────────┘

⸻

5. User Interface Layer

The user interface will provide the primary method of interaction with RTOScope.

The interface is expected to be implemented using a touchscreen display.

Primary UI functions

The interface will provide access to:

* Main system dashboard
* Task monitoring
* Task control
* Scheduler visualization
* Scheduling algorithm demonstrations
* IPC demonstrations
* Synchronization demonstrations
* System resource monitoring
* Hardware demonstrations

The UI should remain responsive while background tasks are executing.

Proposed UI structure

                 RTOScope
                    │
       ┌────────────┼────────────┐
       │            │            │
      Tasks      Scheduler     Monitor
       │            │            │
       ▼            ▼            ▼
   Task List    Timeline      CPU/Memory
   Task State   Algorithms    Task Stats
       ┌────────────┼────────────┐
       │            │            │
      IPC          Sync       Hardware
       │            │            │
       ▼            ▼            ▼
     Queues      Mutexes     Sensors/IO

The exact visual design will be determined during implementation.

⸻

6. RTOScope Core

The RTOScope Core will act as the application-level coordination layer.

Its responsibilities will include:

* Coordinating system modules
* Managing communication between the UI and RTOS functionality
* Maintaining application state
* Requesting system information
* Forwarding user commands
* Coordinating demonstrations

The core should avoid implementing functionality that is already appropriately provided by FreeRTOS.

⸻

7. Task Manager

The Task Manager will provide an interface between RTOScope and the FreeRTOS task system.

Responsibilities

The Task Manager will:

* Track demonstration tasks
* Display task information
* Display task states
* Display task priorities
* Support task suspension/resumption where appropriate
* Support creation/deletion of demonstration tasks where appropriate
* Collect task-related statistics

Conceptual interface

             RTOScope UI
                  │
                  ▼
            Task Manager
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
      Task A    Task B    Task C
        │         │         │
        └─────────┼─────────┘
                  ▼
               FreeRTOS

⸻

8. Scheduler Subsystem

The Scheduler subsystem will have two distinct purposes.

8.1 Embedded RTOS Scheduling

FreeRTOS will be responsible for actual task scheduling on the ESP32.

RTOScope will observe and visualize this behavior.

8.2 Scheduling Algorithm Simulator

RTOScope will also contain a host-based scheduler simulator.

The simulator will allow scheduling algorithms to be implemented and evaluated independently of the physical ESP32.

Initial algorithms:

* First-Come, First-Served (FCFS)
* Round Robin
* Priority Scheduling
* Non-preemptive Scheduling

Simulator architecture

                  Task Input
                      │
                      ▼
              ┌───────────────┐
              │ Task Generator│
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │   Scheduler   │
              └───────┬───────┘
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
        FCFS      Round Robin   Priority
          │           │           │
          └───────────┼───────────┘
                      ▼
              ┌───────────────┐
              │    Metrics    │
              └───────────────┘

The simulator is intended to provide a controlled environment for developing and validating scheduling algorithms before integrating scheduling concepts into the embedded demonstration.

⸻

9. Inter-Task Communication

RTOScope will use FreeRTOS communication mechanisms to demonstrate communication between concurrent tasks.

The initial implementation will use queues.

Example

┌──────────────┐
│ Sensor Task  │
└──────┬───────┘
       │
       │ Data
       ▼
┌──────────────┐
│ FreeRTOS     │
│ Queue        │
└──────┬───────┘
       │
       │ Message
       ▼
┌──────────────┐
│ Processing   │
│ Task         │
└──────────────┘

The UI will provide a method for observing relevant queue activity.

⸻

10. Synchronization

RTOScope will demonstrate synchronization mechanisms used to coordinate concurrent tasks and protect shared resources.

Initial mechanisms:

* Mutexes
* Semaphores

Example shared-resource architecture

        Task A
           │
           ▼
       ┌───────┐
       │ Mutex │
       └───┬───┘
           │
           ▼
   Shared Resource
           ▲
           │
       ┌───┴───┐
       │ Mutex │
       └───────┘
           ▲
           │
        Task B

The exact demonstration will be determined after the initial FreeRTOS prototype is operational.

⸻

11. Interrupt Architecture

Physical hardware events will be used to demonstrate interrupt-driven behavior.

The expected communication path is:

Physical Input
      │
      ▼
Hardware Interrupt
      │
      ▼
Interrupt Service Routine
      │
      ▼
RTOS Notification
      │
      ▼
FreeRTOS Task
      │
      ▼
Application Logic
      │
      ▼
User Interface / Output

Interrupt service routines should perform minimal processing and defer larger operations to appropriate RTOS tasks.

⸻

12. System Monitoring

The System Monitoring subsystem will collect information about the state and performance of the embedded system.

Potential metrics include:

* CPU utilization
* Task runtime
* Task count
* Task states
* Available heap
* System uptime
* Scheduling activity

The monitoring subsystem will provide data to the UI without directly controlling unrelated system components.

Monitoring architecture

                 FreeRTOS
                    │
       ┌────────────┼────────────┐
       ▼            ▼            ▼
     Tasks        Memory       Timing
       │            │            │
       └────────────┼────────────┘
                    ▼
             System Monitor
                    │
                    ▼
                   UI

⸻

13. Hardware Architecture

The ESP32 will serve as the primary processing platform.

The final hardware configuration will be determined during the hardware selection phase.

Planned hardware categories

ESP32
 │
 ├── Touchscreen Display
 │
 ├── Physical Inputs
 │    ├── Buttons
 │    └── Sensors
 │
 └── Physical Outputs
      ├── LEDs
      └── Buzzer / Actuator

The selected components and electrical interfaces will be documented in:

hardware/bill-of-materials.md

and

hardware/pinout.md.

Circuit diagrams will be stored in:

hardware/schematics/

⸻

14. FreeRTOS Task Architecture

The final number of tasks will depend on implementation requirements.

The initial design may include tasks such as:
Demo Task	OS demonstrations	1
Logger Task	Optional event logging	2
Task	Responsibility	Priority
Monitor Task	System statistics	3
Hardware Task	Hardware output/control 4
Sensor Task	Sensor acquisition	5
UI Task	Display and user input	6

Task priorities will be established experimentally and documented during development.

The project will avoid creating unnecessary tasks solely for the purpose of increasing task count.

⸻

15. Communication Between Components

Communication should follow defined interfaces rather than relying on unrestricted shared state.

The general communication model is:

              UI
               │
               ▼
          RTOScope Core
               │
      ┌────────┼────────┐
      ▼        ▼        ▼
    Tasks    Scheduler Monitor
      │        │        │
      └────────┼────────┘
               │
       Queues / Notifications
               │
               ▼
            FreeRTOS

Shared resources shall be protected using appropriate synchronization mechanisms.

⸻

16. Host vs. Embedded Responsibilities

RTOScope will intentionally separate certain development activities between the host computer and the ESP32.

Host Computer

The host environment will be used for:

* Source code development
* Git version control
* Documentation
* Scheduling simulation
* Algorithm development
* Automated testing where practical
* Performance analysis
* Project documentation

ESP32

The ESP32 will be used for:

* FreeRTOS execution
* Real-time task demonstrations
* Hardware interaction
* Interrupt demonstrations
* System monitoring
* User interface
* Embedded performance measurements

This separation allows scheduling algorithms and other logic to be developed and tested before being constrained by embedded hardware.

⸻

17. Data Flow

A typical RTOScope interaction may follow this process:

User
 │
 │ Touches UI
 ▼
UI Task
 │
 ▼
RTOScope Core
 │
 ▼
Task Manager
 │
 ▼
FreeRTOS
 │
 ▼
Target Task
 │
 ├──────────────► Hardware
 │
 └──────────────► Queue / Synchronization
                       │
                       ▼
                  Other Task
                       │
                       ▼
                  System State
                       │
                       ▼
                  Monitor Task
                       │
                       ▼
                       UI

⸻

18. Error Handling

The system should detect and appropriately handle foreseeable failures.

Potential failure conditions include:

* Failed task creation
* Queue creation failure
* Memory allocation failure
* Invalid user input
* Hardware initialization failure
* Invalid scheduling parameters
* Communication errors

Failures should be recorded in the development log and addressed according to their impact on system operation.

⸻

19. Testing Strategy

Testing will occur at multiple levels.

Unit Testing

Individual software components will be tested independently where practical.

Examples:

* Scheduler algorithms
* Scheduling metric calculations
* Task models
* Data structures

Integration Testing

Multiple components will be tested together.

Examples:

* Task manager + FreeRTOS
* UI + Task Manager
* Sensor + Queue + Processing Task
* Interrupt + RTOS Task

Hardware Testing

Physical interfaces will be tested independently before integration.

System Testing

The complete RTOScope system will be tested under realistic demonstration conditions.

Test procedures and results will be documented in docs/testing.md.

⸻

20. Performance Evaluation

RTOScope will evaluate system behavior using measurable performance data.

Potential measurements include:

* Task execution time
* Scheduling latency
* Waiting time
* Turnaround time
* Response time
* CPU utilization
* Memory usage
* Context-switch activity
* Queue utilization

Scheduling algorithms will be compared using controlled workloads where appropriate.

Results will be documented in docs/benchmarks.md.

⸻

21. Planned Repository Relationship

The architecture corresponds to the following major repository components:

RTOScope/
│
├── docs/
│   ├── requirements.md
│   ├── architecture.md
│   ├── hardware-design.md
│   ├── software-design.md
│   ├── scheduling.md
│   ├── ipc.md
│   ├── synchronization.md
│   ├── interrupts.md
│   ├── testing.md
│   ├── benchmarks.md
│   ├── development-log.md
│   └── references.md
│
├── firmware/
│   └── src/
│
├── simulator/
│   └── src/
│
├── hardware/
│   ├── schematics/
│   └── wiring/
│
├── tests/
│
└── assets/

⸻

22. Architectural Decisions Pending

The following decisions remain open and will be resolved during the design and prototyping phases:

* Exact ESP32 model
* Development framework and toolchain
* Display model and communication interface
* Touchscreen implementation
* Sensor selection
* Physical input/output components
* Final task architecture
* FreeRTOS task priorities
* Exact scheduler implementation strategy
* Extent of custom scheduler integration with the embedded system
* Data logging approach
* Final UI framework

These decisions shall be documented as they are made.

⸻

23. Design Philosophy

RTOScope is intended to demonstrate operating system concepts rather than simply provide a collection of hardware features.

Each hardware component should have a meaningful relationship to an operating system concept.

For example:

Button
  ↓
Interrupt
  ↓
RTOS Notification
  ↓
Task
  ↓
Queue
  ↓
Processing Task
  ↓
UI

This approach ensures that hardware and software components contribute to the primary objective of demonstrating real-time operating system behavior.

⸻

24. Revision History

Version	Date	Description
0.1.0	September 4, 2026	Initial architecture specification.

⸻

25. Future Revisions

This document will be updated when major architectural decisions are made or when implementation/testing demonstrates that the current architecture should be modified.

Architectural changes should be recorded in the development log and summarized in the revision history.
