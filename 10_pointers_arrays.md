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

#### Do Now:
  * Turn to your table buddy & discuss what you discovered during last night's homework.
  * Share at least 1 unexpected result.
  * Share at least 1 burning quesrtion you have.

---
template: main

#### Pointer Arithmetic

 * Pointer variables all store unsigned integers and are all the same size. They are still provided types for 2 reasons.
   - de-referencing (`*`) to get the correct value.
   - Pointer arithmetic.

--

 * You can perform the following arithmetic operations on pointers.
   * `+ - ++ --`

--

 * When you perform arithmetic on pointers, the operations are scaled by the size of the pointer type.

---
template: main

#### Array Basics
* An array is an allocated block of memory meant to hold multiple pieces of data of the same type.

--

* C arrays do not have a length attribute/function.

--

* We will use `[]` to access array elements.

--

* The size of an array must be set at declaration and cannot be changed.

--

* The size of an array cannot be dyanmic.

--

* There is no boundry checking (much more on this later).

--

* Array declaraion/access syntax:
 ```C
 float ray[5];
 ray[2] = 8.22;
 ```
* The above code requests a block of memory large enough for 5 `floats` (20 bytes), which then can be accessed using 0-based `[]` notation.

---
template: main

#### Array Variables
* Array _varibles_ (not the arrays themselves) are pointers to the allocated array block.

--

* Unlike standard pointers, array variables are __immutable__, meaning that you can never change the memory address an array variable points to.

--

* In the previous example, `ray` is a variable that points to the beginning of the 20 bytes allocated to that array of floats.

--

* The `sizeof` function can be used to find the size of a given type (like `float` or `char *`), or _the amount of memory associated with a given variable.

--

  * `sizeof(ray)` would return `20`.
  * `sizeof(ray) / sizeof(float)` would return `4`. It is more standard in C _not_ to use this, instead using other constants/variables to keep track of array sizes. Since array sizes must be set at compile time, you're more likely to see something like this:
 ```C
 int ARR_SIZE = 10;
 double trouble[ ARR_SIZE ];
 ```

---
template: main

#### Array Variables & Pointers

- Since array variables are pointers, we can assign normal pointers to array variables.
```C
float ray[5];
float *rp = ray;
```

--

* `ray`, is immutable, so we __could not__ do soemthing like `ray++`, but `rp` is a normal pointer, so we could do `rp++`. Due to _pointer arithmetic_, `rp++` would actually add `4` to `rp`.

--

* `sizeof(ray)` would return `20`, while `sizeof(rp)` would return `8`, since `rp` is a pointer and only holds an 8 byte (on most systems) memory address.

--

* This is commonly done, and because of pointer arithmetic, you can iterate through an array by using a pointer and incrementing it.
---
template: main

#### Array Indexing and `[]` Notation
* The following two pieces of code perform the same task.
 * `ray[3]` and `*(rp + 3)`

--

* In the second example, we add `3` to `rp`, which is the same address as the location for `ray[3]`.

--

* The de-reference operator (`*`), is then used to retrieve the value.

--

* You can think of the standard `[]` notation in terms of specifying an offset from the beginning memory address of an array.

--

* Arrays are 0-indexed because the first element is stored at the starting address, so you need not add to get to the correct memory address.

--

- The `a[i]` notation is actually shorthand for:
  - `*(a + i)`,

--

- This means that you can use `[]` with pointer variables as well.
  - `rp[3]` is valid code.

???
- You can write `ray[-1]` or `rp[-1]`, which would go to the value 4  bytes (one float size) before the beginning of your array.


 * If you use an index past the end of an array allocation, you will be attempting to access the memory addresses past the end of the array.
 * In either case, going past an array allocation on either end is not advised. Your code will compile, but when run, at best you'll access other variables within the program, at worst, you'll crash.


 * __WARNING: HORRIBLE SYNTAX AHEAD__
   * Once again, `*(a + i)` is the same as `a[i]`
   * `+` is a commutative operations, meaning `a + i` == `i + a`
   * ...
   * `*(a + i)` == `*(i + a)`
   * `*(i + a)` == `i[a]`
   * So `ray[2]` can also be written as `2[ray]`. Try it once, then NEVER DO IT AGAIN!
