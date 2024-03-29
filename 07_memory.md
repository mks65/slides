name: main

### .aim[Systems: Making Memories]
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

The repository for assignment 04 was not made over the weekend. It is made now, submit your work today/tonight.

---
template: main

#### Memory: Bits & Bytes

* All digital data is _binary_, broken up into series of 1s and 0s.

* Physically, this data can take many forms, electronic (high voltage \| low voltage), optical (light on \| light off), magnetic (+ \| - magnetic charge) and so on.

* A single 1 or 0 is a __bit__, a unit of digital data.

* 8 bits make a __byte__.

--

* Why 8? - Some people thought that was a good number. It used to be 4.

* If you have a music file that is 5 MB (megabytes) large, that means it takes 5 million bytes, or 40 million bits to be represented digitally. That's 40 million individual 1s and 0s in whatever physical form it may be.

---
template: main

#### Computer Memory 101

* In general, memory is the term used to describe the computer part that contains any active data. Active data includes things like:
  - All open applications, even ones running in the background.
  - All open files.
  - Operating system.
  - Background processes.

--


* The important distinction to be made is between _memory_ and _storage_.
  - _Storage_ refers to data stored on disk (Hard Drive, SSD, Flash Drive, Floppy Disk...).

--
  - Storage is where data gets saved for the long term. At any given time, most computers will have a lot more data in storage than in memory.

--


* Memory is much faster to access than storage, which is why it is used. The downside is that memory is _volitile_, meaning it requires power to retain data.

--

* The most common form of memory is RAM (Random Access Memory). The more RAM you have, the more data you can hape open at once.

???
* Computers can use a concept called _virtual memory_, which will allocate unused disk space for memory purposes in the event that your RAM is full.

---
template: main

#### Computer Memory 101

* When you open a program/file (in the *nix world, everthing is a file), the file is __copied__ from storage into memory. Saving a file reverses this process, taking the changes you've made from memory and copying them into storage.

* Just like any other program, when a program you write is run, it takes up memory space.
* Every variable and function you write gets turned into bits which takes up memory space when run.

* For example, when you declare an `int`, that means your program will request 4 bytes of memory to store a value. How that value is represented is based on __endianness__.

---
template: main

#### Endianness

* In the non-digital world for the number 2,354 we would say 2 is the most significant digit, because that 2 represents 2 thousand, the largest value of any digit in that number.

* Generally, we write decimal numbers left-->right from most-->least significant.

--

* Endianness is a similar concept, except instead of thinking of the significance of digits, we look at the significance of __bytes__.

--

* To store `261` in an `int`, C will use 4 bytes, so it would really look more like this:
  - `00000000` `00000000` `00000001` `00000101`
--


* Systems that use this representation are called __big endian__.

--


* A __little endian__ system use2 the reverse order, going from least to most significant byte.

--

  - `00000101` `00000001` `00000000` `00000000`

???
* Think about the significance of bytes in the same way you think about the significance of digits. In the above representation, the most significant byte comes first. Since we only need 9 bits (which is spread over 2 bytes) to represent `261`, the first two bytes are all `0`. The third byte, `00000001`, represents the number `256`.
*
* Notice that the indicidual bytes are in most->least significant bit order, but the order of the bytes is reversed.
* Another example, `2,151,686,160`
* Big endian: `10000000` `01000000` `00100000` `00010000`
* Little endian: `00010000` `00100000` `01000000` `10000000`
