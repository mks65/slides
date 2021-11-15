name: main

### .aim[Systems: What the Fork?]
<style>
.aim {
font-size: .75em;
border-bottom: 1px solid lightgray;
margin: 1px;
}
.remark-inline-code {
  background-color: lightgray;
  border-radius: 3px;
  padding-left: 2px;
  padding-right: 2px;
}
h4 {
font-size: 1.5em;
margin: 1px;
}
</style>

---
template: main


---
template: main

#### Managing Sub-Processes
- `fork() - <unistd.h>`

  - Creates a separate process based on the current one, the new process is called a child, the original is the parent.

--

  - The child process is a duplicate of the parent process.

--

  - All parts of the parent process are copied, including stack and heap memory, and the file table.

--

  - Returns 0 to the child and the child's pid, or -1 (`errno`), to the parent.

--

  - If a parent process ends before the child, the child's new parent pid is 1

---
template: main

#### Managing Sub-Processes
- `wait - <sys/wait.h>`

--

  - Stops a parent process from running until any child has exited.

--

  - Returns the pid of the child that exited, or -1 (`errno`), and gathers information about the child process (this is called reaping)

--

  - If multiple child processes exit, an arbitrary one will be reaped.

--

  - `wait(status)`
    - `status` is used to store information about how the process exited.

--
    - Status macros
      - Usage: `MACRO( status )`
      - `WIFEEXITED`: True if child exited normally
      - `WEXITSTATUS`: The return value of the child
      - `WIFSIGNALED`: True if child exited due to a signal
      - `WTERMSIG`: The signal number intercepted by the child

---
template: main

#### Managing Sub-Processes

- `waitpid - <sys/wait.h>`
  - Wait for a specific child
  - `waitpid(pid, status, options)`
    - `pid`
      - The pid of the specific child to look for
      - If -1, will wait for any child (normal wait)
  - `options`
    - Can set other behavior for waitpid, if 0, will work normally.
