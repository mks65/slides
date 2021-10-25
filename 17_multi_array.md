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

#### Two Dimensional Arrays

* `int bigray[2][4];` Declares a 2-d array of ints.
  - 32 bytes (2 * 4 * sizeof(int)) are allocated sequentially.

--

  - `bigray[r]` refers to a single row, in dereference notation:
    - `*(bigray + r)`
    - In pointer arithmetic, `r` is multiplied by the appropriate size.
    - The size in this case is __4 * sizeof(int)__ becuase that is the size of each row.

--
  - `bigray[r][c]` refers to an element, in dereference notation:
    - `*(bigray + r)[c]`
      - Here, `r` is still multiplied by __4 * sizeof(int)__
      - Because `[]` takes presidence over `*`, this then becomes
      - `**(bigray + r) + c)`.
      - But `c` is multiplied by __sizeof(int)__


#### Two Dimensional Arrays and Pointers

* Because indexing notation requires knowing the size of a row, pointers and 2-d arrays do not work as seamlessly as pointers and 1-d arrays.

* `int **bp = bigray` will compile, but will not work as desired. Since the type of `bp` is `int **`, the pointer arithmetic will only be based on sizeof(int *), instead of the size of a row.

--
  - `bp[r][c]` becomes `**(bp + r + c)`
    - but r is scaled by __sizeof(int *)__, instead of __4 * sizeof(int)__
