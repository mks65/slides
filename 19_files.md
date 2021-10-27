name: main

### .aim[Systems: File This Under Useful Information]
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

#### Everything is a File

* Famously, in *nix operating systems (which includes macOS), "Everything is a File".

> The whole point with "everything is a file" is not that you have some random filename (indeed, sockets and pipes show that "file" and "filename" have nothing to do with each other), but the fact that you can use common tools to operate on different things. -Linus Torvalds

--

* Understanding how to interact with normal files in code will allow you to work with other less "file-y" things like removeable media, speakers, monitors, microphones, network connections ...


---
template: main

#### File permissions

- 3 types of permissions that determine how you can interact with a file.

--

  - read, write, execute

--

- Permissions can be represented as 3-digit binary #s, or 1-digit octal #s
  - 100 <==> 4 => read only
  - 111 <==> 7 => read, write, execute

--

- There are 3 permission “areas"

--

  - user, group, others

--

  - Membership in each area is mutually exclusive.

  - The creator of the file is the default setting for the user and group of a file.

  - Each area can have its own permissions

---
template: main

#### File permissions

- `chmod permissions file`
  - Command line utility to change file permissions.
  - The owner of a file (or root) can change permissions.
  - File ownership and group can be changed with the `chown` and `chgrp` command line utilities.

---
template: main

#### File Table

- A list of all files being used by a program while it is running.

--

- Contains basic information like the file's location and size.

--

- The file table has limited space, which is a power of 2 and commonly 256.

--

  - `getdtablesize()` will return the file table size.

--

- Each file is given an integer index, starting at 0, this is the __file descriptor__.

--

- There are 3 files always open in the table:
  - `0` or `STDIN_FILENO`: `stdin`
  - `1` or `STDOUT_FILENO`: `stdout`
  - `2` or `STDERR_FILENO`: `stderr`

---
template: main

#### File functions
- `open - <fcntl.h>`

  - Add a file to the file table and returns its file descriptor.
  - If open fails, -1 is returned, extra error information can be found in `errno`.
    - `errno` is an int variable that can be found in `<errno.h>`
    - Use `strerror` (in `string.h`) on errno to return a string description of the error
  - `open( path, flags, mode )`
    - `mode`
      - Only used when creating a file. Set the new file's permissions using a 3 digit octal #
    - `flags`
      - Determine what you plan to do with the file, use the following constants and combine with `|`:
      - `O_RDONLY`, `O_WRONLY`, `O_RDWR`, `O_APPEND`, `O_TRUNC`, `O_CREAT`
      - `O_EXCL`: when combined with `O_CREAT`, will return an error if the file exists

---
template: main

- `umask - <sys/stat.h>`
  - Set the file creation permission mask
  - By default, created files are not given the exact permissions provided in the mode argument to open. Some permissions are automatically shut off.
  - Umask is applied the following way:
    - `new_permissions = ~mask & mode`
    - The linux default mask is `0002`.
  - `umask(mask)`;
- `read - <unistd.h>`
  - Read data from a file
  - `read( fd, buff, n )`
    - Read `n` bytes from `fd`'s file into `buff`
    - Returns the number of bytes actually read. Returns -1 and sets `errno`	if unsuccessful.
    - `buff` must be a pointer.
- `write - <unistd.h>`
  - Write data to a file
  - `write( fd, buff, n )`
    - Write `n` bytes to the `fd`'s file from `buff`
    - Returns the number of bytes actually written. Returns -1 and sets `errno`	if unsuccessful.
    - `buff` must be a pointer.
