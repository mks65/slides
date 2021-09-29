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

#### Endianness

* In the non-digital world for the number 2,354 we would say 2 is the most significant digit, because that 2 represents 2 thousand, the largest value of any digit in that number.

* Generally, we write decimal numbers left-->right from most-->least significant.

--

* Endianness is a similar concept, except instead of thinking of the significance of digits, we look at the significance of __bytes__.

--

* To store `261` in an `int`, C will use 4 bytes, so it would really look more like this:
  - `00000000` `00000000` `00000001` `00000101`
--


* Systems that use this representation are called __big endian__.

--


* A __little endian__ system use2 the reverse order, going from least to most significant byte.

--

  - `00000101` `00000001` `00000000` `00000000`

???
* Think about the significance of bytes in the same way you think about the significance of digits. In the above representation, the most significant byte comes first. Since we only need 9 bits (which is spread over 2 bytes) to represent `261`, the first two bytes are all `0`. The third byte, `00000001`, represents the number `256`.
*
* Notice that the indicidual bytes are in most->least significant bit order, but the order of the bytes is reversed.
* Another example, `2,151,686,160`
* Big endian: `10000000` `01000000` `00100000` `00010000`
* Little endian: `00010000` `00100000` `01000000` `10000000`


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

* You can get the address of any variable using the __address of operator__: `&`

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
template: main

#### Pointers

* Regular variables are designed to store _values_.

* Pointers are variables designed to store _memory addresses_.

--

* Pointers are variables, meaning they are an identifier for a value stored in memory at a particular address.

--

* Pointers must be able to store the value of any potential memory address. On 64 bit computers, this means pointers have to be able to represent 64 bits, or 8 bytes.

--

* Pointers are designed for addresses, which means they are natively `unsigned`.

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
