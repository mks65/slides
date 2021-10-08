name: main

### .aim[Systems: Constructing Data]
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
better gh repo setup
source code now available: https://github.com/mks65/dwsource, link on site

---
template: main

#### Structs

* A custom data type that is a collection of values.

--

* The following line creates a variable, `s`, who's type is an anonymous struct:
 * `struct { int a; char x; } s;`

--

 * `struct { int a; char x; }` is the full type of `s`, it is syntactically identical to `int` or `float` ...

--

* We use the `.` operator to access a value inside a struct
 * `s.a = 10;`
 * `s.x = ‘@‘;`

--

???
* Here is an example of creating and using a struct:
 ```C
 int main() {
     struct {int a; char x;} s0;

     s0.a = 51;
     s0.x = '%';

     printf("s0: %d\t%c\n", s0.a, s0.x);

     return 0;
  }
 ```

---
template: main

#### Structs

* It is preferable to __prototype__ your structs, which will make it easier to create and work with multiple variables of the same struct type.

 * `struct foo { int a; char x; };`

--

 * Note that since we are not creating a variable, there is no name between the `}` and the `;` at the end.

--

* After creating a prototye for a struct, you can declare new variables of that type like so:
 * `struct foo s;`
 * You still must include the word `struct`.

--

- It is typically better practice to prototype structs outside of any particular function.

* Struct prototypes are most commonly found in .h files.

???
* Here is an example of creating and using a struct with a prototype:
 ```C
 struct foo {int a; char x;};

 int main() {

     struct foo s0;
     struct foo s1;

     s0.a = 51;
     s0.x = '%';

     s1 = s0;
     printf("s0: %d\t%c\n", s0.a, s0.x);
     printf("s1: %d\t%c\n", s1.a, s1.x);

     return 0;
  }
 ```
---
template: main

#### Pointers and Structs

* You can make pointers to structs like pointers to primitaves.
 * `struct foo *p = &s;`

--

* One very important note, `.` takes precedence over `*`.

--

 * This means that `*p.x` is the same as `*(p.x)` which is almost certainly __NOT__ what you want. (This will look for x inside p and de-reference that result).

--

 * To access a value in a struct via a pointer you need to do: `(*p).x`, that is, de-reference first, then get x.
 * In C, `p->x` is syntactic shorthand for `(*p).x`

---
template: main

#### Stack memory vs Heap memory

- Every program can have its own stack and heap.

--

- __Stack memory__
  - Stores all normally declared variables (including pointers and structs), arrays and function calls.

--

  - Functions are pushed onto the stack in the order they are called, and popped off when completed.

--
  - When a function is popped off the stack, the stack memory associated with it is released.

--

- __Heap memory__
  - Stores dynamically allocated memory.

--

  - Data will remain in the heap until it is manually released. (or the program terminates)
