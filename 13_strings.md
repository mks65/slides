name: main

### .aim[Systems: Strings!]
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

#### Strings in C

* Strings are character arrays.

--

* By __convention__ the last entry in a string character array is the NULL character (either `0`, the number, or `\0`, the character).

--

* This is __not guranteed__, if you want to create a string, you will need to make sure that there is a terminating NULL.

--

* When you use `""` to make a string _literal_:
  1. A character array large enough to store the string, including a terminating NULL, is created in memory.
  2. The characters of the string are stored in that array, and a terminating NULL is added.

--

* String literals are _immutable_.

* If a string literal is exactly repeated in code, a new character array is not created, instead, the orginal array is used. This means all references to the same immutable string literal refer to the same piece of memory.


---
template: main

#### Declaring Strings

* There are 4 ways to declare strings in C

--

* `char s[256];`
   * Declares a mutable array of 256 bytes.
   * No speciic characters are saved to memory.
   * No guarantee of a NULL character at any position.

--

* `char s[256] = "Imagine"`
   * Creates the immutable string literal `"Imagine"`.
   * Declares a mutable array of 256 bytes.
   * __Copies__ the string `"Imagine"`, including a terminating NULL, into the first 8 bytes of the array `s`.

---
template: main

#### Declaring Strings

* `char s[] = "Tuesday";`
   * Creates the immutable string literal `"Tuesday"`.
   * Creates an 8 bytes array, large enough for `"Tuesday"` and a terminating NULL for the variable `s`.
   * __Copies__ the string `"Tuesday"`, including a terminating NULL, into the array `s`.

--

4. `char *s = "Mankind";`
   * Creates the immutable stirng literal `"Mankind"`.
   * `s` becomes a pointer to that immutable string.
   * `s` is just a pointer to the memory location with the immutable string lives. If you want a mutable string, you cannot declare it this way.

---
template: main

#### Working With String Variables

* It is important to keep track of _variables_ vs. _values_.
* `char s[10] = "Yankees";`
  - `s` is an array variable that points to the 10 byte array allocation.
  - `s` is immutable, it cannot point to any other memory location.

--
  - `s = "Mets";` __is an error__.
--

  * The values in the array `s` points to are __not__ immutable. You can change the value of the string at any point.

--
  * `s[0] = 'M';` is ok.
--

* `char *s = "AL East Champions";`
  * Here, `s` is a pointer.

--
  * As a pointer, you can change the value `s` points to.
  * `s = "The Best";` is valid.

--
  * Since `s` points to an immutable string literal, you cannot change the value of the string.
  * `s[0] = 'N';` __is an error__.
