name: main

### .aim[Systems: A Bit 'o Wisdom]
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

#### Binary, Octal and Hexadecimal Integers
  - Other base formatting characters for printf:
    - `%o`: octal integer
    - `%x`: hexadecimal integer

--

  - You can define native integers in bases 2, 8 and 16 by using the following prefixes
    - `0b` : binary
    - `0` : octal
    - `0x` : hexadecimal
    - THIS DOES NOT CHANGE THE VALUE
      - `0b1101 == 015 == 0xD == 13`

---
template: main

#### Bitwise Operators

  - Evaluated on every bit of a value
  - `~x`
    - Negation
    - Flip every bit of x.

--

  - `a | b`
    - Bitwise or
    - Perform logical or for each pair of bits in (a, b)

--

  - `a & b`
    - Bitwise and
    - Perform logical and for each pair of bits in (a, b)

--

  - `a ^ b`
    - Bitwise xor
    - Perform logical xor for each pair of bits in (a, b)

---
template: main

#### Bitwise Operators

  - `x >> n`
    - Right shift
    - Move all the bits of x to the right n spaces.
    - Fill in 0s on the left side.
    - n must be positive, if x is negative, the result is machine dependent.

--

  - `x << n`
    - Left Shift
    - Move all the bits of x to the left n spaces.
    - Fill in 0s on the right side.
    - n must be positive, if x is negative, the result is undefined.
  - Left shift and Right shift will not overflow end bits into adjacent memory.
  - Generally, they work well with unsigned numbers, and get tricky with negative values.


---
template: main

#### xor swap

???

  1. a = a ^ b;
  2. b = a ^ b;
  3. a = a ^ b;
  - xor is commutative and associative
  1. q = a ^ b
  2. r = q ^ b
  3. s = q ^ r
  2. r = (a ^ b) ^ b
     - r = a ^ (b ^ b)
     - r = a ^ 0
     - r = a
  3. s = (a ^ b) ^ a
     - s = (a ^ a) ^ b
     - s = 0 ^ b
     - s = b
