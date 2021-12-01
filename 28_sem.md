name: main

### .aim[Systems: Capture the Flag]
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

<div class=" middle center">
<video width="560" height="420" controls>
    <source src="assets/monty_python_semaphore.mp4" type="video/mp4">
</video>
</div>

---
template: main

#### Semaphores

(created by Edsger Dijkstra)

IPC construct used to control access to a shared resource (like a file or shared memory).

--

Most commonly, a semaphore is used as a counter representing how many processes can access a resource at a given time.
- If a semaphore has a value of 3, then it can have 3 active “users".
- If a semaphore has a value of 0, then it is unavailable.

--

Most semaphore operations are _atomic_, meaning they will not be split up into multiple processor instructions.

---
template: main

#### Semaphores

__Semaphore operations__
- "Maintenance operations"
  - Create a semaphore
  - Set an initial value
  - Remove a semaphore

--

- Traditional Semaphore Usage

  - `Up(S)` \| `V(S)` - _atomic_
    - Release the semaphore to signal you are done with its associated resource
    - Pseudocode
      - `S++`

--

  - `Down(S)` \| `P(S)` - _atomic_
    - Attempt to take the semaphore.
    - If the semaphore is 0, wait for it to be available
    - Pseudocode
      - `while (S == 0) { block } S--;`

---
template: main

#### Semaphores in C
- `<sys/types.h> <sys/ipc.h> <sys/sem.h>`
- `semget`
  - Create/Get access to a semaphore.
  - Returns a semaphore descriptor or -1 (`errno`)
  - `semget( key, amount, flags )`
    - `key`
      - Unique semaphore identifier
    - `amount`
      - Semaphores are stored as sets of one or more. The number of semaphores to create/get in the set.
    - `flags`
      - `IPC_CREAT`: create the semaphore and set value to `0`
      - `IPC_EXCL`: Fail if the semaphore already exists and `IPC_CREAT` is on.
      - Includes permissions for the semaphore, combine with bitwise or (`|`).

---
template: main

#### Semaphores in C

- `semctl`
  - Control the semaphore, including
    - Set the semaphore value
    - Remove the semaphore
    - Get the current value
    - Get/set semaphore metadata
  - `semctl(descriptor, index, operation, data)`
    - `descriptor`
      - The return value of `semget`
    - `index`
      - The index of the semaphore you want to control in the semaphore set.
    - `operation`
      - `IPC_RMID`: remove the semaphore
      - `SETVAL`: Set the value (requires data)
      - `GETVAL`: Return the value
---
template: main

#### Semaphores in C
  - `data`
    - Variable for setting/storing semaphore metadata
    - Type is `union semun`
    - __You have to declare this union in your main c file on linux machines.__
      - ```
        union semun {
          int val;                  //used for SETVAL
          struct semid_ds *buf;     //used for IPC_STAT and IPC_SET
          unsigned short  *array;   //used for SETALL
          struct seminfo  *__buf;
        };
        ```
    - `union`?
      - A c structure designed to hold only one value at a time from a group of potential values.
      - Just large enough to hold the largest piece of data it could potentially contain

---
template: main

#### Semaphores in C
- `semop`
  - Perform an atomic semaphore operation
  - You can `Up/Down` a semaphore by any integer value, not just `1`
  - `semop( descriptor, operation, amount )`
    - `amount`
      - The amount of operations you want to perform on the semaphore set.
    - `operation`
      - A pointer to a `struct sembuf`
        - ```
          struct sembuf {
            short sem_op;
            short sem_num;
            short sem_flag;
          };
          ```
        - `sem_num`
          - The index of the semaphore you want to work on.
        - `sem_op`
          - `Down(S)`: Any negative number
          - `Up(S)`: Any positive number
          - `0`: Block until the semaphore reaches `0`
        - `sem_flag`
          - `SEM_UNDO`: Allow the OS to undo the given operation. Useful in the event that a program exits before it could release a semaphore.
          - `IPC_NOWAIT`: Instead of waiting for the semaphore to be available, return an err



# ftok
- `<sys/ipc.h>`
- Generate a key useful for IPC functions
- `ftok( path, x )`
  - `path`
    - A path to some file, the file must be accessible by the program.
  - `x`
    - An int used to generate the key
  - The same path and x will always generate the same key
