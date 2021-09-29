name: main

### .aim[Systems: Get to the Point]
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

#### Makefiles Revisited

* You can run the rules for a specific target with `$ make TARGET`

--

* rules do not need to always involve compilation. Common non-compiling targets include:

--

  - `run`: run the created program.

--

  - `clean`: remove unnecessary files (.o, ~, etc)

???
show euler

add euler.h to euler.c, get into #ifndef thing.

---
template: main

#### Pointers

* Even though all pointers are the same size, we declare them using the type of the value pointed to.

--

* `*` is used to declare a pointer variable.
  - `int *p = &x;`
  - `p` is a pointer variable that stores the address of the variable `x`.

--

* In Java, object variables, or references, are essentially pointers, called references instead.

--
  - The exception you get when you try to use an uninitialized object variable in Java is _null pointer_, meaning the reference stored is 0 (null), which is an invlaid memory address.

---
template: main

#### Pointers

* Consider the following C snippet:
```C
unsigned int i = 2151686160;
int *ip = &i;
char *cp = &i;
```

- `ip` and `cp` will store the address of the first byte used to store `i`. Depending on the _endianness_ of the system, that byte will either be `10000000` (big) or `00010000` (little).

--

* Let's just say that the first byte is located at memory address `3000` (using small number for ease of discussion)

--

* If you perform `ip++` and `cp++`, each pointer will be incremented by 1, but due to pointer arithmetic, `ip` will increase to `3004` and `cp` will increase to `3001`. In essence, `ip` would move one `int` forward in memory, while `cp` only moves one byte forward.


---
template: main

#### Pointers

* `*` is also used as the __de-reference operator__. This will return the value stored at the memory address pointed to by the pointer.

--

* Given the definitions of `x` and `p` above:

--

* `int y = *p + 10;` would set `y` to the value `15`.

--

* `*p = y;` would set the value at the memory address stored in `p` (in the example is 2000), to whatever the value stored in `y` is.
