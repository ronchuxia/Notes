# Process, Process Group and Session
## Process
A process is a program in execution.

A process has a **PID** (process identifier).
## Process Group
A process group is a collection of related processes.

A process group has a **PGID** (process group identifier). PGID is the PID of the process that created the group (i.e. the **process group leader**).

Child processes usually inherit their parent processes' PGID, unless they create a new process group.
## Session
A session is a collection of one or more process groups.

 A session has a **SID** (session identifier).
 
 When a new session is created, a new process group is created in that session, its PGID is set to the PID of the process that created the session (i.e. the **session leader**).

# Starting a Process
## `fork()`
`fork()` creates a new process. 

`fork()` makes a copy of the current process. The child gets a copy of the parent’s memory, file descriptors, environment, current working directory, etc. The parent process and the child process both continue running from the line after `fork()`. The return value tells them apart.
```cpp
pid_t pid = fork();

if (pid == -1) {
	std::cerr << "fork failed\n";
	return 1;
}

if (pid == 0) {
	std::cout << "child process\n";
} else {
	std::cout << "parent process, child pid = " << pid << "\n";
}
```

## `execve()`
`execve()` replaces the current process with a new program.

```cpp
pid_t pid = fork();

if (pid == -1) {
	std::cerr << "fork failed\n";
	return 1;
}

if (pid == 0) {
    // child
    execve("/bin/ls", argv, envp);
} else {
    // parent
    waitpid(pid, NULL, 0); // wait for child to finish
    printf("child finished\n");
}
```

# Stopping a Process
`SIGTERM`, `SIGKILL`, and `SIGINT` are signals used to tell a process to stop.

| **Signal** | **Number** | **Meaning**                                 | **Can process handle/ignore it?** | **Typical source**   |
| ---------- | ---------- | ------------------------------------------- | --------------------------------- | -------------------- |
| `SIGTERM`  | 15         | Ask the process to terminate gracefully.    | Yes                               | `kill <pid>`         |
| `SIGKILL`  | 9          | Force the process to terminate immediately. | No                                | `kill -9 <pid>`      |
| `SIGINT`   | 2          | Interrupt the process.                      | Yes                               | `Ctrl+C` in terminal |

# Process Lifecycle
## Zombie Process
A **zombie process** is a process that has finished running, but whose parent has not collected its exit status using `wait()`, `waitpid()`, etc. 

A zombie process does not use CPU or memory, but it still occupies a process table entry.
## Orphan Process
An **orphan process** is a process that is still running, but whose parent has exited.

An orphan process is adopted by `systemd` (PID 1) or a subreaper (e.g. a service manager process, a container runtime process, etc.).
