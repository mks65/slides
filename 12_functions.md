name: main

### .aim[Systems: Take Me to Funky Town]
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

#### Do Now

Join the (currently empty) google classroom for this class using the following code:

### kvzzvji

???
github submodule stuff
dont use private repos, seem to not work

check the repositories, i've had to remove directories for each assignment.

HW Review! Marc, Cameron
---
template: main

#### C Functions
* All functions in C are _pass by value_.
 * This means that the arguments are __copied__ into new variables when the function is called.

--

 * As a result, normal values are not modified when passed into a funtion.

--

```C
void swap(int a, int b) {
  int t = a;
  a = b;
  b = t;
}
```

--

```C
void swap(int *a, int *b) {
  int t = *a;
  *a = *b;
  *b = t;
}
```
???
   * In this example, when `swap` is run on `x` and `y`, `a` and `b` are created. The function swaps the values of `a` and `b`, but once the function finishes, it is popped off the call stack, and `a` and `b` are gone. `x` and `y` are left unchanged.
 * This is where pointers come in handy. If you pass a pointer to a memory address, then you can modify the value it points to. Look at this modified version of swap.

   * Now that `swap` takes pointers, we can de-reference the parameters to get at the values pointed to. When the function is colled, `a` and `b` become copies of the _adrresses_ of `x` and `y`, so when `swap` finishes, the values will actaully be swapped.
   *


---
template: main

#### Functions, Pointers and Arrays

* Passing pointers as arguments is what happens in Java when object variables are used, you may recall the phrase _pass by reference_, all that means is pass by value, but the value being passed is a memory address.

--

* When you pass an array as a argument to a function, the entire array is _not_ copied.

--

* All arrays are treated as regular pointers when passed into a function. The following function headers are equivalent:
   * `void arr_func( int arr[]);`
   * `void point_func( int *arr);`

--

   * It is generally preferred to use the second option, since it makes clear that the parameter is a normal pointer.
