name: main

### .aim[Systems: ]
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

#### Memory Addresses

* In order to understand pointers, we need to take a closer look at variables.

* There are three key features to any variable in your code:
  1. The __identifier__: Name you use in code to refer to the variable.

--
  2. The __value__: Data that you store.

--
  3. The __address__: The location of data in memory.

--


* Let's focus on the __address__.

* Memory is addressed by starting at the first byte block (1), going up until the last accessible byte.

--

* The amount of potential memory addresses is limited by the processor.

--

* The address space of a program is determined by the operating system (OS), when the program is run. Therefore it can be different each time.

--

* You can get the address of any variable using the __address of operator__: `&`;

???
* For example, if your computer has 4GB of RAM, then in theory memory addresses would go from 1 to ~32,000,000,000.


* since a processor must be able to read an entire memory address within a single cycle.

* For modern, 64-bit computers, this means you could theorhetically have 2^64 bytes of memory, though this number is practically limited by hardware.

---
template: main

#### Interacting With Addresses

* The `%p` placeholder character will print out a memory address in hexadecimal format: `printf("x: %d, address of x: %p\n", x, &x);`.

--

* If you would prefer to see the address in decimal, you can use the placeholder for an `unsigned long`. (This will most likely result in a warning from gcc): `printf("x: %d, address of x: %lu\n", x, &x);`.

--

* Revisitng `printif`:

  * `%d` : print a value as a signed decimal `int`.
  * `%u` : print a value as a decimal `unsigned int`.
  * `%o` : print a value as an octal number.
  * `%x` : print a value as a hexidecimal number.
    - `%o` and `%x` will always treat the value as if it were unsigned.

--

* The following characters can be used to modify `u`, `d`, `o` or `x`:

--
  * `h` : modify the printed value to look at 2 bytes instead of 4.
  * `hh` : modify the printed value to look at 1 byte.

???
* You can print a value out with `%u` or `%d` regardless of how it is declared, that doesn't mean it will make sense, just that `printf` will convert the value accordingly.


* The code snippet below displays these options:
```C
unsigned int q = 2151686160;
printf("%%d: %d\n", q);
printf("%%u: %u\n", q);
printf("%%o: %o\n", q);
printf("%%x: %x\n", q);
printf("%%hhx: %hhx\n", q);
printf("%%hhu: %hhu\n", q);
```
* When run, this prints (on my computer):
```
%d: -2143281136
%u: 2151686160
%o: 20020020020
%x: 80402010
%hhx: 10
%hhu: 16
```
* Things to notice:
* `%d` is not the actual value we used, this has to do with how negative numbers are represented.
* `%hhx` and `%hhu` print the first byte of the value. Based on that, you can tell the endianness of the system the program is run on (it is possible you get a different result from my example).

---

### Pointers - now the fun really starts.
* Regular variables are designed to store _values_.
* Pointers are variables designed to store _memory addresses_.
* Pointers are variables, meaning they are an identifier for a value stored in memory at a particular address (see above for detail), the only difference is that a pointer is designed to store an address.
* Pointers must be able to store the value of any potential memory address. On 64 bit computers, this means pointers have to be able to represent 64 bits, or 8 bytes.
* Pointers are designed for addresses, which means they are natively `unsigned`.
* Even though all pointers are the same size, we declare them using the type of the value pointed to.
* `*` is used to declare a pointer variable.
* `int *p = &x;`
* Here `p` is a pointer variable that stores the address of the variable `x`.
* Notice that p is a normal variable, and has its own, different, memory address.
* If you're thinking, "hey, this looks familiar... like object variables in java". You're right! Object variables, or references, are java's pointers. You just don't have as much control over them as we do in C. In fact, think about the error you get when you try to use an uninitialized object variable in java... _null pointer_, meaning the reference stored is 0 (null), which is an invlaid memory address.
* `*` is also used as the __de-reference operator__. This will return the value stored at the memory address pointed to by the pointer.
* Given the definitions of `x` and `p` above:
* `int y = *p + 10;` would set `y` to the value `15`.
* `*p = y;` would set the value at the memory address stored in `p` (in the example is 2000), to whatever the value stored in `y` is.








* Back to the whole pointer thing, consider the following C snippet:
```C
unsigned int i = 2151686160;
int *ip = &i;
char *cp = &i;
```
* `ip` and `cp` will store the address of the first byte used to store `i`. Depending on the _endianness_ of the system, that byte will either be `10000000` (big) or `00010000` (little).
* Let's just say that the first byte is located at memory address `3000` (using small number for ease of discussion)
* If you perform `ip++` and `cp++`, each pointer will be incremented by 1, but due to pointer arithmetic, `ip` will increase to `3004` and `cp` will increase to `3001`. In essence, `ip` would move one `int` forward in memory, while `cp` only moves one byte forward.
