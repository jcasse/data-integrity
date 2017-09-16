[//]: # (Markdown: dillinger.io/ shows a nice example of Markdown commands with a viewer.)
[//]: # (Comments in Markdown: http://stackoverflow.com/questions/4823468/comments-in-markdown)
[//]: # (C++ Project Structure: http://hiltmon.com/blog/2013/07/03/a-simple-c-plus-plus-project-structure/)
[//]: # (C++ Library Creation: http://www.adp-gmbh.ch/cpp/gcc/create_lib.html)

# Data Integrity Tester

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

### Installation

```sh
$ git clone git@github.com:jcasse/data-integrity-tester.git
$ cd data-integrity-tester
$ make
```
### Usage

```sh
$ bin/data-integrity-tester --help

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
```

License
----

[//]: # "A short snippet describing the license (MIT, Apache, etc.)"

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
