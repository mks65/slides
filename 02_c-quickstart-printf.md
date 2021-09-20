name: main

### .aim[Systems: The Basics, printf]

<style>
.aim {font-size: .75em}
.remark-inline-code {
  background-color: lightgray;
  border-radius: 3px;
  padding-left: 2px;
  padding-right: 2px;
}
h4 {font-size: 1.5em}
</style>

<hr>
---
template: main

#### C Basics
* C program files are _mostly_ a series of function definitions. As C is not an OOP language, there is no class-like structural overhead.

* Like in Java, `main` is a special function, it is the only function that runs at program execution. Any functions called from within `main` will also be run.
* C is a _statically typed language_, meaning identifiers (variables and functions) must be given a type when they are declared.
    * The types are similar to those in Java, with a few notable exceptions.
    * For the moment, use `int` for integers and `double` for floating point values.
* `main` should have a return type of `int`. This can be used later on to check if a program executed successfully. By convention, a return value of `0` means everything went as planned.

---
template: main

#### Writing, compiling, and running
 * By convention, C source files should have a `.c` file extension (i.e. `dylan.c`).

 * The C compiler we will be using is __gcc__ (the Gnu C Compiler)
   * usage: `$ gcc dylan.c`
     * This will create a standalone executable file.
     * The default name for the output file is `a.out`
     * There is no preferred extension for c executable files.
     * You can provide your own output file name with the `-o` flag.
       * usage: `$ gcc -o dj dylan.c`

 * Compiled C programs are natively executable, to run them just type `./program` (i.e. `$ ./a.out` or `$ ./dj`
   * The `./` is only needed because you probably compiled the file in a folder outside your PATH environment variable.

---

#### `printf`
- `printf` is the function normally used in C to print to standard out.

- usage: `printf( string, arg0, arg1, ...)`
  - Sends `string` to standard out.
* The first argument must be a literal string enclosed by `"`.

--

* `string` can contain special placeholder characters that are used to insert other values into the output.

--

* If placeholder characters are used, then they will be replaced by the arguments following the string when `printf` is executed.

--

* The value arguments can be either variables or literal values.
  - example: `printf(“these are numbers: %d %lf\n”, 3, 845.273);` would display: `these are numbers: 3 845.273`

---

#### `printf` Formatting Characters

 | Type | Placeholder |
 |------|-------------|
 |`int` | `%d`        |
 |`long`| `%ld`       |
 |`float`| `%f`*       |
 |`double`| `%lf`*     |
 |`char`| `%c`         |
 |string| `%s` |
 |pointer| `%p`|

 \* `%0.xf` or `%0.xlf` will print `x` significant digits after the floating point

`printf` will attempt to interpret any value with the provided formatting character, even if they do not match.

---

#### Variables and Types

* All C primitives are numeric. The only differences are floating point vs. integer and size of variable in memory.

* Size can be platform dependent
  * `sizeof(type)` can be used to find the size in bytes (`stdlib.h`)

| Type | Size (bytes) | Range |
|------|------|-------|
|`char`   | 1  | -128 --> 127  |
|`short`   | 2  | -32,768 —-> 32,767  |
|`int`   | 4  | -2<sup>31</sup> --> 2<sup>31</sup>-1   |
|`long`   | 8  | -2<sup>63</sup> --> 2<sup>63</sup>-1   |

--
|`float`   | 4  | 7 digits of precision  |
|`double`   | 8  | 14 digits of precision  |

--

* Variables can be declared as `unsigned`. Unsigned variables do not use a bit to store the sign of the number, making the lower bound 0 and increasing the upper bound.

--

- All variables must be declared before being used.

--

- __Variables are not given initial values.__
