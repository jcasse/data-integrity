## Synopsis

[//]: # (At the top of the file there should be a short introduction and/ or overview that explains **what** the project is. This description should match descriptions added for package managers (Gemspec, package.json, etc.))

This program checks for data integrity and retention on storage devices.
It writes data chunks that contain certain information used for verification.

Chunk data fields:
LBA - logical block address (offset into partition in multiples of block size)
GEN - chunk genration number (number of times the block was written)
TIM - timestamp of last write to block
RID - run id (unique identifier for this test)

Verification:
During the verification phase the LBA and GEN values are compared to what is
expected. For example, if the program writes LBA 3 seven times, then the
program expects that when it reads LBA 3, it has 7 for the GEN number.

In case that the data does not match what is expected, the other pieces of
information in the data chunk can give a hint to what might have caused the
data corruption.

## Code Example

[//]: # (Show what the library does as concisely as possible, developers should be able to figure out **how** your project solves their problem by looking at the code example. Make sure the API you are showing off is obvious, and that your code is short and concise.)

Usage:
 datint [options] file

Options:

 -h            print this menu

 -s            seed for random number gen. (default is 0)

 -m            random LBA (default is serialized)

 -r            read-only (default is read/write)

 -w            write-only (default is read/write)

 -x            random w/r (default is read/write)

 -b <number>   beginnig LBA (default is 0)

 -e <number>   bounding LBA (default is file size)

 -i <number>   number of test iterations (default is 1)

 -z <number>   i/o block size (multiple of default 512)

Example uses:

Serialized writes and reads. First write all LBAs and then read them back for
verification.

datint /dev/sda3

Randomized writes and reads. Do writes and reads at random. If trying to read
a block that was not previously written, the program will instead write the
block.

datint -x /dev/sda3

Like above, but randomize the blocks as well.

datint -x -m /dev/sda3

Specify block range.

datint -b 3 -e 37 /dev/sda3

Specify i/o block size (block size must be a multiple of 512).

datint -z 1024 /dev/sda3

## Motivation

[//]: # (A short description of the motivation behind the creation and maintenance of the project. This should explain **why** the project exists.)

To better understand solid state memory hardware.

## Installation

[//]: # (Provide code examples and explanations of how to get the project.)

TODO

## API Reference

[//]: # (Depending on the size of the project, if it is small and simple enough the reference docs can be added to the README. For medium size to larger projects it is important to at least provide a link to where the API reference docs live.)

TODO

## Tests

[//]: # (Describe and show how to run the tests with code examples.)

TODO

## Contributors

[//]: # (Let people know how they can dive into the project, include important links to things like issue trackers, irc, twitter accounts if applicable.)

TODO

## License

[//]: # (A short snippet describing the license (MIT, Apache, etc.))

[//]: # (http://choosealicense.com/)

Copyright (C) 2016 Juan Casse

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

