# Rate Monotonic Scheduling with Aperiodic Tasks

Real-time scheduling of periodic and aperiodic tasks with POSIX threads on Linux, using **Rate Monotonic** priorities (`SCHED_FIFO`) on a single CPU. Two strategies are compared for the aperiodic tasks: background scheduling and a polling server.

> First assignment of the Real-Time Operating Systems course (1st year, 1st semester), MSc Robotics Engineering, University of Genoa.

## Content

Starting from the course example (3 periodic and 2 aperiodic tasks), one periodic and one aperiodic task were added.

| File | Aperiodic tasks | Periodic tasks (period) |
|---|---|---|
| `RM_aperiodic_background.c` | Threads with the lowest priority, woken up through condition variables | 100, 200, 400, 500 ms |
| `RM_polling_server.c` | Executed by a **polling server**, a periodic thread with the highest priority that serves a queue of requests | server 50 ms; tasks 100, 200, 400, 500 ms |

Both programs:
1. estimate the execution time of every task;
2. check schedulability with the utilization test (U ≤ U<sub>lub</sub>), including the server capacity in the polling version;
3. create one thread per periodic task with Rate Monotonic priorities, pinned to CPU 0;
4. at run time, task 1 randomly requests the aperiodic tasks, and the execution order is printed on the terminal.

## Usage

Requires Linux and root privileges, needed to set `SCHED_FIFO` priorities.

```bash
g++ RM_polling_server.c -lpthread -o polling_server
sudo ./polling_server

g++ RM_aperiodic_background.c -lpthread -o background
sudo ./background
```
