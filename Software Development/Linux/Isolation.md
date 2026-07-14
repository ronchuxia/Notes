# Control Group
A **cgroup (control group)** limits how much system resources a process can use.

# Namespace
In Linux, a **namespace** is an isolation mechanism, it changes what a process can **see** or **operate on** for a kind of system resource.
## PID Namespace
**PID namespace** isolates process IDs. It affects the process tree **visibility** to a process.
## User Namespace
**User namespace** isolates user IDs and group IDs. It affects the user and group **identity** and thus **permission** of a process.
## Mount Namespace
**Mount namespace** isolates the filesystem mount table. It affects the filesystem view **visibility** to a process.