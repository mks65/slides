name: main

### .aim[Systems: Sharing Is Caring]
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

#### Inter-Process Communication (IPC)

There are many kinds of Inter-Process Communication, _but_ there is a specific set of IPC features that have competing standardized implementations, these are:
  * Shared Memory
  * Semaphores
  * Message Queues

--

For these features, there are 2 standards:
  * Portable Operating System Interface (POSIX)
  * System V
  * Both of these cover more than IPC.

--

POSIX and System V provide the same features, just via a different set of function calls. We will use System V.

???
POSIX: A cross-platform specification supported by UNIX operating systems and those considered UNIX-like, such as Linux. The X in the name originally denoted that the interface was “based on UNIX.”

System V: The specification that defines the requirements for an operating system to be considered UNIX.



---
template: main

#### Shared Memory

A segment of heap-like memory that can be accessed by multiple processes.

Shared memory is accessed via a key that is known by any process that needs to access it.

Shared memory does not get released when a program exits.

--

- __5 Shared memory operations__
  - Create the segment (happens once) - `shmget`
  - Access the segment (happens once per process) - `shmget`
  - Attach the segment to a variable (once per process) - `shmat`
  - Detach the segment from a variable (once per process) - `shmdt`
  - Remove the segment (happens once) - `shmctl`

---
template: main

#### System V Shared Memory Operations

Headers: `<sys/shm.h> <sys/ipc.h> <sys/types.h>`

```C
int *data;
int shmd;
shmd = shmget(KEY, sizeof(int), IPC_CREAT | 0640);
printf("shmd: %d\n", shmd);
data = shmat(shmd, 0, 0);
printf("data: %p\n", data);
printf("*data: %d\n", *data);
*data = * data + 10;
printf("*data: %d\n", *data);
shmdt(data);
```
