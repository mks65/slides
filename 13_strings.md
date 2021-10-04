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


# Strings in C
  * Strings are character arrays.
  * Everything we went over yesterday with respect to arrays is the same. There is nothing special about the way character arrays work. Becuase strings are so useful, there are a few features of C that make working with them simpler.
  * By __convention__ the last entry in a string character array is the NULL character (either `0`, the number, or `\0`, the character). This is not something that is guranteed, if you want to create a string, you will need to make sure that there is a terminating NULL, if not, a number of string related functions will not work.
  * When you use `""` to make a string _literal_:
    1. A character array large enough to store the string, including a terminating NULL, is created in memory.
    2. The characters of the string are stored in that array, and a terminating NULL is added.
  * String literals are _immutable_.
  * If a string literal is exactly repeated in code, a new character array is not created, instead, the orginal array is used. This means all references to the same immutable string literal refer to the same piece of memory.

  # Declaring Strings
  * There are 4 ways to declare strings in C (in eaxch example, the numbers and strings used are randomly chosen, none have special meaning in C).
  1. `char s[256];`
     * Declares a mutable array of 256 bytes.
     * No speciic characters are saved to memory.
     * No guarantee of a NULL character at any position.
  2. `char s[256] = "Imagine"`
     * Creates the immutable string literal `"Imagine"`.
     * Declares a mutable array of 256 bytes.
     * __Copies__ the string `"Imagine"`, including a terminating NULL, into the first 8 bytes of the array `s`.
  3. `char s[] = "Tuesday";`
     * Creates the immutable string literal `"Tuesday"`.
     * Creates an 8 bytes array, large enough for `"Tuesday"` and a terminating NULL for the variable `s`.
     * __Copies__ the string `"Tuesday"`, including a terminating NULL, into the array `s`.
  4. `char *s = "Mankind";`
     * Creates the immutable stirng literal `"Mankind"`.
     * `s` becomes a pointer to that immutable string.
  * It is important to note that in example 4, an array is not created. In that case `s` is just a pointer to the memory location with the immutable string lives. If you want a mutable string, you cannot declare it this way.

  # Working With String Variables
  * Everything we've covered about pointers and arrays still holds true, string variables are pointers, either array pointers or normal pointers.
  * It is important to keep track of _variables_ vs. _values_.
    * `char s[10] = "Yankees";`
      * In this example, `s` is an array variable that points to the 10 byte array allocation. `s`.
      * `s` is immutable, it cannot point to any other memory location.
        * `s = "Mets";` __is an error__.
      * The values in the array `s` points to are __not__ immutable. You can change the value of the string at any point.
        * `s[0] = 'M';` is perfectly good.
    * `char *s = "AL East Champions";`
      * Here, `s` is a pointer.
      * As a pointer, you can change the value `s` points to.
        * `s = "The Best";` is valid.
      * Since `s` points to an immutable string literal, you cannot change the value of the string.
        * `s[0] = 'N';` __is an error__.
