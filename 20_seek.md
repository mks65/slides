name: main

### .aim[Systems: Seek and Ye Shall Find]
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
--

  - If open fails, -1 is returned, extra error information can be found in `errno`.
--

    - `errno` is an int variable that can be found in `<errno.h>`
    - Use `strerror` (in `string.h`) on errno to return a string description of the error
--

- `open( path, flags, mode )`
  - `mode`
      - Only used when creating a file. Set the new file's permissions using a 3 digit octal #
--
  - `flags`
      - Determine what you plan to do with the file, use the following constants and combine with `|`:
--
      - `O_RDONLY`, `O_WRONLY`, `O_RDWR`, `O_APPEND`, `O_TRUNC`, `O_CREAT`
      - `O_EXCL`: when combined with `O_CREAT`, will return an error if the file exists

---
template: main

#### File functions

- `umask - <sys/stat.h>`
  - Set the file creation permission mask

  - By default, created files are not given the exact permissions provided in the mode argument to open. Some permissions are automatically shut off.

--

  - Umask is applied the following way:
      - `new_permissions = ~mask & mode`
      - The linux default mask is `0002`.
    - `umask(mask)`

---
template: main

#### File functions

- `read - <unistd.h>`
  - Read data from a file
  - `read( fd, buff, n )`
    - Read `n` bytes from `fd`'s file into `buff`
    - Returns the number of bytes actually read. Returns -1 and sets `errno`	if unsuccessful.
    - `buff` must be a pointer.

--

- `write - <unistd.h>`
  - Write data to a file
  - `write( fd, buff, n )`
    - Write `n` bytes to the `fd`'s file from `buff`
    - Returns the number of bytes actually written. Returns -1 and sets `errno`	if unsuccessful.
    - `buff` must be a pointer.
