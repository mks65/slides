name: main

### .aim[Systems: Make it so]
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

#### Compiling and Linking

* Compilers are more complex than straightforward source code --> executable code translators, and have multiple components.

* To start, we'll look at three major pieces of gcc:
  - __preprocessor__
    - `gcc -E` will only run the preprocessor, can view the output text.
  - __compiler__
    - `gcc -c` will run all steps up to and including the compiler.
  - __linker__

---
template: main

- `#ifndef IDENTIFIER ... #endif`
  - Conditional preprocessor statement.
  - If `IDENTIFIER` is not defined (for the preprocessor), then include all the lines of code up to the `#endif`.
  - If `IDENTIFIER` is defined, skip everything up to the `#endif`.
- Example
  ```C
  #ifndef PI
  #define PI 3.14159
  #endif
  ```

---
template: main

#### Compiler
- Turns C source code into binary code.

- The result is __not__ an executable program.

--

- Only one C file is compiled at a time.

--

- The compiler checks called functions against their declared hearders, but if a function is defined in a separate file, its code is __not added__ at this step.

--

- `$ gcc -c <FILE>` will run the preprocessor and compile stages only, creating a non executable binary object file. The resulting file will have an extension of __.o__.

- Since an executable is _not_ created, you can successfully compile, via `$ gcc -c`, a C file that does not have a `main` function.

---
template: main

#### Linker
- Combines compiled binary code from multiple files into a single executable program.

--

- Will automatically look for standard library source code, or anything that can be included using `<>`.

--

- If multiple definitions for any identifier is found, the linker will fail.

--

- Must find __one__ definition for `main`.

--

- If you provide gcc multiple c files, it will compile each one individually and then run the linker on them together.

--

- If you provide gcc any .o files, it will skip the compilation step for those files and then use them during linking.

---
template: main

- You can mix and match .c and .o files for gcc, but it is not encouraged.

--

- Instead, this would be a good way to compile a program, if you had files `foo.c goo.c boo.c`:
 - `$ gcc foo.c goo.c boo.c`

--
 - or:
    ```bash
    $ gcc -c foo.c
    $ gcc -c goo.c
    $ gcc -c boo.c
    $ gcc -o program foo.o goo.o boo.o
    ```

---

#### Make
  * Command line tool to help automate building programs with multiple files and dependencies.

  * Only compiles files that have been modified, or that rely on modified files.

--

  - Compiling instructions and file dependencies are put into a _makefile_.

  * Running `$ make`, will look for a file called _makefile_ (you can specify a different file with the `-f` flag).

  * The main parts of makesfiles are:

   * Targets: Things to make (usually executables or .o files)

--

    - Dependencies: Files or other targets needed to create a target.

--
   * Rules: How to create the target.

---
#### Make
- Make will always run the first target.

--
- Make recursively goes through dependencies.

--
- Make will check the modification timestamps for __targets__ and __dependencies__ and will only run the __rules__ if the target is older than one or more of its dependencies.

--
- Makefile Syntax:
  ```make
  target: dependency0 dependency1 dependency2 ...
  TAB rule
  ```
* There should be a newline between the dependency list and the rules, and the __TAB__ is necessary, there should not be any space between it and the rule.

---
### Make

  * Here is a makefile for a program made from three .c files: main.c, foo.c and goo.c.
   * main.c calls functions from foo.c
   * foo.c calls functions from goo.c
     ```make
     all: main.o foo.o goo.o
         gcc -o program main.o foo.o goo.o

     main.o: main.c foo.h
         gcc -c main.c

     foo.o: foo.c foo.h goo.h
         gcc -c foo.c

     goo.o: goo.c goo.h
         gcc -c goo.c
       ```
   * This makefile creates the executable file __program__.
   * Since _all_ is not a file and it is the first target, it will always run.
???
     * If instead, the first target was called __program__, then make would check the modification timestamp of that file.
   * __main.o__ is the first dependency, so make will go to that target.
   * __main.o__ depends on main.c and foo.h
   * The rest of the dependencies will go through in a similar way. Running `$ make` the first time would do the following:
     ```
     gcc -c main.c
     gcc -c foo.c
     gcc -c goo.c
     gcc -o porgram main.o foo.o goo.o
     ```
   * Notice the order of compilation and trace it through the makefile.
   * If goo.h is modified, the following would happen:
     ```
     gcc -c foo.c
     gcc -c goo.c
     gcc -o porgram main.o foo.o goo.o
     ```
