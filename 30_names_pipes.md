name: main

### .aim[Systems: A pipe by any other name...]
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

center_img {
  display: block;
  text-align: center;
}
</style>

---
template: main

#### Named Pipes

Also known as FIFOs.

--

Same as unnamed pipes except FIFOs have a name that can be used to identify them via different programs.

Like unnamed pipes, FIFOS are unidirectional.

--

`mkfifo`
- Shell command to make a FIFO
- `$ mkfifo name`

---
template: main

#### Named Pipes in C
`mkfifo - <sys/types.h> <sys/stat.h>`

- `mkfifo( name, permissions )`

- c function to create a FIFO

- Returns 0 on success and -1 on failure

--

- Once created, the FIFO acts like a regular file, and we can use `open`, `read`, `write`, and `close` on it.

--

- FIFOs will __block on open__ until both ends of the pipe have a connection.
