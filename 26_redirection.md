name: main

### .aim[Systems: The Art of Redirection]
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

#### File Redirection

Changing the usual input/output behavior of a program

--

Command line redirection

- `>`
  - Redirects stdout to a file.

--
  - Overwrites the contents of the file.

--
- `>>`
    - Redirects stdout to a file by appending.

--

- `<`
  - Redirect stdin from a file.
  - The file is treated exactly like stdin, for example `fgets()` will read up until a newline is found.

---
template: main

Redirection in c programs

- `dup - <unistd.h>`
  - Duplicates an existing entry in the file table.
  - Returns a new file descriptor for the duplicate entry.
  - `dup( fd )`

--
- `dup2 - <unistd.h>`
  - `dup2( fd1, fd2 )`
  - Redirects `fd2` to `fd1`
  - Any use of `fd2` will now act on the file for `fd1`.

--

- USING `dup` and `dup2` together:

  ```C
  fd1 = open(“foo”, O_WRONLY);
  backup_sdout = dup( STDOUT_FILENO ) // save stdout for later
  dup2(fd1, STDOUT_FILENO) //sets STDOUT_FILENO's entry to the file for fd1.
  dup2(backup_stdout, STDOUT_FILENO) //sets STDOUT_FILENO’s entry to backup_stdout, which is stdout
  ```
