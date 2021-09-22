name: main

### .aim[Systems: Gettin' Funky]
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

--

   * Quick note on `for`: Do not declare your counter variable in the loop.
     * `for( x=0; x < 10; x++)` Totally cool.
     * `for( int x=0; x < 10; x++)` no bueno.

--

 * Remember that in C, __all numbers are boolean values__, 0 is false, everything else is true.
   * `if ( x = 0 )`

--

   * C interprets this statement as follows:
	 1. Assign variable x the value 0.

--

	 2. The assignment operator returns the value assigned, so the statement will return 0.

--

	 3. 0 is false, so the if statement will fail.

---
template: main

### Declaring and Defining Functions
  * Function and variable names are both examples or _identifiers_.

  * All identifiers must be declared before they can be used.

  * A function declaration provides its return type, name and parameters. This is also known as a function _header_.

    - `double dylan(int jack);`

---
template: main

### Programming Time!
* Look at the problems here: http://projecteuler.net/index.php?section=problems
* They are all math problems of some sort, pick two and write a c program to solve them
  - Write a function for each problem you solve.
    - The function should return the solution.
    - In `main`, call each function and print out the results.
  * Some good starters are problems 1, 5 and 6
  * Finished early? pick a third, [a fourth, a fifth](https://youtu.be/y8AWFf7EAc4?t=92)...
