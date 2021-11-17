* Compress Data using Huffman Compression

Learning Goals
==============

* Understand bitwise operations

* Compress data using Huffman codes

Compress Data
=============

Continue from HW14, after you build the compression tree, you have
the codes of the characters. The following is an example


```
A 65 00
m 109 010
# 35 0110
G 71 0111
c 99 10
s 115 11
```

Next, consider the end of an article with the following characters:

`Acss#Gcsm...`

`A` should become code `00`. 

`c` should become code `10`.

`s` should become code `11`.

`s` should become code `11`.

Thus, the first 8 bits (first byte) are `00101111`.

`#` should become code `0110`.

`G` should become code `0111`.

Thus, the second 8 bits (second byte) are `01100111`.

The first three types will be 

`00101111 01100111 1011010 ...`

Spaces are added between bytes for clarity, do not add space in your
program's output.

Please use `xxd -b` to inspect the bits in a binary file.

This assignment gives you the end of an article using the
characters in the compression tree.  This assignment uses only the
end of an article, not the entire article, so that the input is
shorter and debugging may be easier.  You can assume that the article
is actually longer than the given test input.  Your program needs to
compress the characters using bits. If some bits in the last byte are
unused, make the unused bits zero. 

What Does Your Program Do
=========================

Your program should take three inputs from the command-line argument:

* `argv[1]` is name of the file that describes the tree (HW14's input)

* `argv[2]` is name of the file that contains data (new for this HW)

* `argv[3]` is the name of the output (binary) file

This is an example:

From `argv[1]`, the input file is 

`1A1m1#1G0001c1s000`

HW14 builds the compression tree and finds the codebook:

```
#:0110
A:00
G:0111
c:10
m:010
s:11
```

The second input file (`argv[2]`) has `#AcGms#Ac`.  From the code book, this is the codes for the data:

Character | #    | A  | c  | G    | m   | s  | #    | A  | c  
----------|------|----|----|------|-----|----|------|----|----
Code      | 0110 | 00 | 10 | 0111 | 010 | 11 | 0110 | 00 | 10

Next, we put 8 bits together into one byte. This is the output
(`argv[3]`) of the program (in bits). This file should have only 4
bytes.

`01100010 01110101 10110001 00000000`

That is the output of this program. If you use `xxd -b`, it shows

`00000000: 01100010 01110101 10110001 00000000`

You can assume that the compression tree in `argv[1]` is valid and all
characters in `argv[2]` appear in the compression tree.


Submission
==========

Please submit all necessary files. These are the requirements:

* You must include `Makefile`. Without `Makefile`, it is not possible building your program.

* The executable must be called `hw15` and must not be called anything else.

* Your program should take three arguments as described above.

* Your program must not have any unwanted output. Unwanted output will
  be treated as errors.


