# Thread Scheduler Project Plan

## Table of Contents
1. [Project Overview](#project-overview)
2. [Research and Foundations](#research-and-foundations)
3. [The Basic Library](#the-basic-library)
4. [Synchronization: Mutexes](#synchronization-mutexes)
5. [Scheduling Algorithms](#scheduling-algorithms)

---

## Project Overview
A user-level thread library made to understand POSIX threads. The best way to learn something is the make it!

## Research and Foundations
* **Read Documentation:** Understand the project requirements.
* **Master `ucontext`:** Focus on `swapcontext` for switching between execution flows.

## The Basic Library
### Implementation Notes
* **Scheduler Context:** Needed for handling context swaps.
* **Main Thread Context:** Needed for benchmarks and returning to the entry point.

### Data Structures
* **TCB (Thread Control Block):** Defined in `thread_worker_type.h`.
* **Context:** Each TCB holds a `ucontext`.
* **RunQueue:** A list of TCBs that are ready to run.

### Core Functions
* **`worker_create()`**: Mallocs the stack (`SIGSTKSZ`) and uses `makecontext()`.
* **`worker_yield()`**: Voluntarily pauses the current thread.
* **`worker_exit()`**: Saves return value and cleans up the TCB.
* **`worker_join()`**: Blocks the current thread until the target thread exits.

## Synchronization: Mutexes
* **`worker_mutex_init()`**: Initialize the lock.
* **`worker_mutex_lock()`**: Locks the mutex or blocks the thread if held.
* **`worker_mutex_unlock()`**: Unlocks and wakes up waiting threads.
* **`worker_mutex_destroy()`**: Cleanup; ensure lock is free before destroying.

## Scheduling Algorithms
### First Come First Serve (FCFS)
* Baseline implementation.
* No preemption.

### Round Robin (RR)
* FCFS with preemption.
* **Quantum:** Fixed time limit per thread.
* **Implementation:** Use `sigaction()` and timers to trigger the scheduler handler.