name: main

### .aim[Systems: A Heap o'Trouble]
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

---
template: main

#### Dynamic memory allocation

- `malloc(size_t x)`
  - Allocates x bytes of heap memory.

--

  - Returns the address at the beginning of the allocation

--

  - Returns a void *
      ```
      int *p;
      p = malloc( 5 * sizeof(int) );
      ```

--

- `free(void * p)`
  - Releases dynamically allocated memory.
  - Has one parameter, a pointer to the beginning of a dynamically allocated block of memory.
  - Every call to malloc/calloc should have a corresponding call to free.

---
template: main

- `calloc(size_t n, size_t x)`
  - Allocates n * x bytes of memory, ensuring every bit is 0.
  - Works like malloc in all other ways
      ```
      int *p;
      p = calloc( 5, sizeof(int) );
      ```

--

- `realloc(void *p, size_t x)`
  - Changes the amount of memory allocated for a block to x bytes.
  - `p` must point to the beginning of a block.

--

  - Returns a pointer to the beginning of the block.

--

  - If `x` is smaller than the original size of the allocation, the extra bytes will be released.

--

  - If `x` is larger than the original size then either:
    - If there is enough space at the end of the original allocation, the original allocation will be updated.
    - If there is not enough space, a new allocation will be created, containing all the original values. The original allocation will be freed.
