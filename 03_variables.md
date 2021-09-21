name: main

### .aim[Systems: Variables are the Spice of Life]

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

#### Do Now: Try this in a C program:

* Declare and initialize an `int`, `float` and `char`.

* Print out the values of those variables correctly.

* Then print out the values using incorrect formatting characters.

---
template: main

#### Primitive Types

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

* `char` is an integer type, but can be used to refer to character literals as well.
  * `char c = 97;` and `char c = 'a';` are both equally valid statements.
  * This also means you can perform arithmetic operations on chars natively.

--
* Note there is no boolean type. In c, any number is a boolean value:
  * __0 is false__
  * __All other numeric values are true__

---
template: main

#### Variables
* Variables must be declared before they are used.
   * You can assign a variable a value at declaration (i.e. `int x = 10;`)
--

* _THERE IS NO DEFAULT VALUE FOR VARIABLES_
  * Declaring a variable means requesting a piece of memory to be used by your program of the corresponding variable size.
  * If you do not initialize (provide a value for) a variable, it's initial value will be whatever happens to be in the piece of memory that was assigned to your variable.
--

* Variables can be declared as `unsigned`. Unsigned variables do not use a bit to store the sign of the number, making the lower bound 0 and increasing the upper bound.


---
template: main

#### Control Structures
 * C has the same basic control structures as java: `if, else if, else, while, for, do ... while`
   * Quick note on `for`: Do not declare your counter variable in the loop.
     * `for( x=0; x < 10; x++)` Totally cool.
     * `for( int x=0; x < 10; x++)` no bueno.
--

 * Remember that in C, __all numbers are boolean values__, 0 is false, everything else is true.
   * `if ( x = 0 )`

--

   * Upon first glance, maybe it seems fine, maybe you notice the incredibly common programming typo.

--

   * javac would never let this fly. Then again, javac assumes you are an idiot and that you have no idea how to program.

--

   * gcc thinks this is totally cool. gcc thinks you are a master programmer (perhaps even a 1337 hax0r), and you meant to do this.
--

   * C interprets this statement as follows:
     1. Assign variable x the value 0.
     2. The assignment operator returns the value assigned, so the statement will return 0.
     3. 0 is false, so the if statement will fail.
