name: main

### .aim[Systems: Directory Listings]
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

???
- `lseek - <unistd.h>`
  - Set the current position in an open file
  - `lseek( file_descriptor, offset, whence )`
    - `offset`
      - Number of bytes to move the position by, Can be negative.
    - `whence`
      - Where to measure the offset from
      - `SEEK_SET`: offset is evaluated from the beginning of the file
      - `SEEK_CUR`: offset is relative to the current position in the file
      - `SEEK_END`: offset is evaluated from the end of the file
  - Returns the number of bytes the current position is from the beginning of the file, or -1 (`errno`)

---
template: main

#### File functions

- `stat - <sys/stat.h>	`
  - Get information about a file (metadata)

--

- `stat( path, stat_buffer )`
  - `stat_buffer`
    - Must be a pointer to a `struct stat`
    - All the file information gets put into the stat buffer.

--

  - Some of the fields in struct stat:
    - `st_size`: file size in bytes
    - `st_uid, st_gid`: user id, group id
    - `st_mode`: file permissions
    - `st_atime, st_mtime`: last access, last modification

--
      - These are `time_t` variables. We can use functions in `time.h` to make sense of them
      - `ctime( time )`
        - Returns the time as a string
        - `time` is type `time_t *`

---
template: main

#### Directories

- A *nix directory is a file containing the names of the files within the directory along with basic information, like file type.

--

- Moving files into/out of a directory means changing the directory file, not actually moving any data.

--

- `opendir - <dirent.h>`
  - Open a directory file
  - This will not change the current working directory (cwd), it only allows your program to read the contents of the directory file

--

  - `opendir( path )`
    - Returns a pointer to a directory stream (`DIR *`)

--

- `closedir - <dirent.h>`
  - Closes the directory stream and frees the pointer associated with it.
  - `closedir( dir_stream )`

---
#### Directories

- `readdir - <dirent.h>`
  - `readdir( dir_stream )`
  - Returns a pointer to the next entry in a directory stream, or `NULL` if all entries have already been returned.

--

- `struct dirent - <sys/types.h>`
  - Directory struct that contains the information stored in a directory file. Some of the data members
  - `d_name`: Name of a file
  - `d_type`: File type as an int

--

- `rewinddir - <dirent.h>`
  - `rewinddir(d)`
    - `d` must be a `DIR *` returned from `opendir`
    - Resets the directory stream of `d` to the beginning.

???
  - Example usage:
      ```
      DIR * d;
      d = opendir( "somedir" );
      struct dirent *entry;
      entry = readdir( d );
      closedir(d);
      ```
