---
layout: default
title: "Better perf scoping"
excerpt: "To better scope the gathered `perf` stats we can run the tool from the code instead of the terminal..."
---

# Better perf scoping

Often it is need to troubleshoot performance issues at a specific region of a program rather than the entire program. To achive profiling of exact region the following snippets of code are helpful:

```cpp
#include <signal.h>
#include <sys/wait.h>

pid_t run_perf() {
    pid_t pid = fork();
    if (pid != 0)
        return pid;
    const auto parent_pid = std::to_string(getppid());
    std::cout << "Running perf on parent process " << parent_pid << std::endl;
    execlp("perf",
           "perf",
           "record",
           "-F999",
           "-g",
           "--call-graph",
           "dwarf",
           "-p",
           parent_pid.c_str(),
           (char*)nullptr);
    throw std::runtime_error(std::string("perf failed: ") + std::strerror(errno));
}

void stop_perf(pid_t perf_pid) {
    printf("Sent SIGTERM to the perf\n");
    kill(perf_pid, SIGTERM);
    int status = 0;
    printf("Waiting the perf\n");
    waitpid(perf_pid, &status, 0);
    printf("The perf has terminated\n");
}

void benchmarked() {
    auto const perf_pid = run_perf();
    
    // the code
    
    stop_pid(perf_id);
}
```

What happens here is that instead of running the `perf` from the terminal we run it from the benchmarked code. We run the perf right before the code of interest and kill it right after it.
