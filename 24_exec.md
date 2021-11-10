name: main

### .aim[Systems: Executive Decision]
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

Today, after 10th period in this very room, Mike Zamansky, creater of our CS program, and curent head of Hunter College's Honors CS program, will give a talk about what stuyding CS in college is like. He will also speak about the Hunter program, but the main focus will be CS in general. If you are thinking at all about persuing CS, it would be a worthwhile talk to attend.

---
template: main

#### String Parsing

- `strsep - <string.h>`
  - Parse a string with a common delimiter
  - `strsep( source, delimiters )`
  - Locates the first occurrence of any of the specified delimiters in a string and replaces it with `NULL`

--

  - `delimiters` is a string, each character is interpreted as a distinct delimiter.

--

  - Returns the beginning of the original string, sets source to the string starting at 1 index past the location of the new `NULL`

  - Since `source`’s value is changed, it must be a pointer to a string `(char **)`.

--

  - example
    ```
    char line[100] = "woah-this-is-cool";
    char *curr = line;
    char * token;
    token = strsep( &curr, "-" );
    ```
    - replaces the `-` after woah with `NULL`
    - returns a pointer to the `w` in `“woah"`
    - sets `curr` to point to the `t` in `"this-is-cool"`

---
template: main

#### The exec family - `<unistd.h>`

- A group of c functions that can be used to run other programs.

--

- Replaces the current process with the new program.

--

- `execl`
  - `execl(path, command, arg0, arg1 … NULL)`
  - `path`
    - The path to the program (ex: `"/bin/ls"` )
  - `command`
    - The name of the program (ex: `"ls"`)
  - `arg0` …
    - Each command line argument you wish to give the program. (ex `"-a", “-l"`)
    - The last argument must be `NULL`

---
template: main

#### The exec family - `<unistd.h>`

- `execlp`
  - `execlp(path, command, arg0, arg1 … NULL)`
  - Works like `execl`, except it uses the `$PATH` environment variable for commands.
  - For example, you can use "`ls`" as the `path` instead of `“/bin/ls"`
  - To check the `$PATH` environment variable, use: `$ echo $PATH`

--

- `execvp`
  - `execvp(path, argument_array)`
  - `argument_array`
    - Array of strings containing the arguments to the command.
    - `argument_array[0]` must be the name of the program.
    - The last entry must be `NULL`
    - Like `execlp`, the path argument will use the `$PATH` environment variable.
