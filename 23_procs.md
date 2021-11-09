name: main

### .aim[Systems: Trust in the Process]
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

#### Processes

- Every running program is a process.

--

- A process can create subprocesses, but these are no different from regular processes.

--

- A processor can handle 1 process per cycle (per core).

- "Multitasking" appears to happen because the processor switches between all the active processes quickly.

--

- On *nix style machines, processes are also files, listed in the `/proc` directory.

--

- __pid__
  - Every process has a unique identifier called the pid.
  - pid 1 is the init process
  - `getpid() - <unistd.h>`
      - returns the current process' pid
  - `getppid() - <unistd.h>`
      - returns the current process' parent pid

---
template: main

#### Signals
  - Limited way of sending information to a process, specifically, an integer.
--

  - `$ kill`
    - Command line utility to send a signal to a process
--
    - `$ kill pid`
      - Sends signal 15 (`SIGTERM`) to `pid`
--
    - `$ kill -signal pid`
      - Sends `signal` to `pid`

--
  - `$ killall [-signal] process_name`
    - Sends `SIGTERM` (or `SIGNAL` if provided) to all processes with `process_name`

---
template: main

#### Signals in c programs
- All these functions can be found in `<signal.h>`
- `kill(pid, signal)`
  - Returns 0 on success or -1 (`errno`) on failure.
  - Works like the command line `kill` program

--

- `sighandler`
    - To intercept signals in a c program you must create a signal handling function.
--

  - Some signals (like `SIGKILL`, `SIGSTOP`) cannot be caught.
--

  - `static void sighandler( int signo )`
    - Must be `static`, must be `void`, must take a single `int` parameter.
--
    - `static`
      - Static values in c exist outside the normal call stack, they can be accessed regardless of the function at the top.
      - For variables, this also means they retain their value even if the function they are declared in has ended.
      - Static values (variables and functions) can only be accessed from within the file they are declared.

---
template: main

#### Signals in c programs

- `signal`
  - Attach a signal to a signal handling function
  - `signal( SIGNUMBER, sighandler)`
  - Note that you are passing the name of the signal handling function as a parameter.
- singal/sighandler example:
  ```C
  static void sighandler(int signo) {
  if ( signo == SIGUSR1 )
  printf("Who you talkin to?\n”);
  }
  …
  signal(SIGUSR1, sighandler);
  ```
