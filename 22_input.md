name: main

### .aim[Systems: Input]
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

#### Command Line Arguments:

- `int main( int argc, char *argv[] )`

  - Program name is considered the first command line argument

--

  - `argc`
    - number of command line arguments

--

  - `argv`
    - array of command line arguments as strings

---
template: main

#### Pulling data from strings
- `sscanf - <stdio.h>`

--

  - Reads in data from a string using a format string to determine types.

--

  - `sscanf( char *s, char * format, void * var0, void * var1, ...)`

--
    - Copies the data into each variable.

--
    - example
    ```
    int x; float f; double d;
    sscanf(s, ”%d %f %lf", &x, &f, &d);
    ```
---
template: main

#### stdin input

* Your OS determines the behavior of the _standard input stream_. Usually:
  - It captures data input via the keyboard as chracters.
  - It is a buffered file stream. This means that data will remain inside standard in until the data is read.
  - The enter key will send a newline character, but will also automatically trigger a program to read from standard in.

--

* The Standard input device (`/dev/stdin`) is a automatically open when a program starts at file descriptor `STDIN_FILENO`.

* You can use `read` to get input from standard in.
  - `read(STDIN_FILENO, buffer, sizeof(buffer))`

---
template: main

#### `fgets`

* Becasue standard in is not a normal file, and is buffered by definition, it is preferatble to use buffered operations on it, specifically `fgets`

- `fgets - <stdio.h>`
  - Read in data from a _file stream_ and store it in a string.

--

  - `fgets( char * s, int n, FILE * f );`
    - Reads at most `n-1` characters from _file stream_ `f` and stores it in `s`, appends `NULL` to the end.

--
    - Stops at newline, end of file, or the byte limit.

--
    - File steam
      - `FILE *` type, more complex than a file descriptor, allows for buffered input.
      - `stdin` is a `FILE *` variable provided when your program starts.

--

- `fgets(s, 100, stdin)`
