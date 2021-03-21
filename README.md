# hex2bin

## An Intel Hex to binary file converter for Elf/OS

I was trying to come up with a project for my first foray into file
handling under Mike Riley's Elf/OS, and came across a couple of "it'd
be nice to have an Intel Hex to binary converter that ran under Elf/OS"
messages on the mailing list. The light bulb came on, and a day later,
hex2bin was born.

hex2bin converts the Intel Hex filename given on the command line to
its binary counterpart. If the filename ends with a 3 character
extension of any name, the output file name is the truncated file name.
In all other cases, an extension of '.bin' is added.

```
   $ hex2bin test.hex
   test created
   $
```	

The code verifies each line's checksum, and handles gaps in the hex
file by padding with FFs. It also checks for overlapping addresses and
flags them as an error. The error reporting is extremely basic.

The source was assembled with a modified version of the
[A18 assembler](https://github.com/carangil/A18) that includes *push*
and *pop* pseudo ops. The header files `bios.inc` and `kernel.inc` are
slightly modified versions of Mike Riley's files; the `#ifdef...#endif`
bits have been removed or unconditionally included as appropriate,
`#define`s changed to `equ`, and upper/lower casing was made consistent.
