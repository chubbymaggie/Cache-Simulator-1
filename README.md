# Cache Simulator #


We learned a bit about caches in the [Computer Systems Fundamentals](http://gaming.jhu.edu/~phf/2015/fall/cs233/) course 
at [Johns Hopkins University](https://www.jhu.edu). This repository contains a cache simulator that reads a memory access
trace and then simulates the behavior of a cache configured with specific parameters.

#### Random Access Trace: An Example ####

The following is an example of a random access trace. Another example can be found in this repository, listed as small.trace.
```
s 0x1fffff50 1
l 0x1fffff58 1
l 0x1fffff88 6
l 0x1fffff90 2
l 0x1fffff98 2
l 0x200000e0 2
l 0x200000e8 2
l 0x200000f0 2
l 0x200000f8 2
l 0x30031f10 3
s 0x3004d960 0
s 0x3004d968 1
```

Each memory access performed by a program is recorded on a separate line. There are three "fields" seperated by white space.
The first field is either ```l``` or ```s``` depending on whether the processor is loading from or storing to memory. 
The second field is a 32-bit memory address given in hexadecimal.

#### Configuration Parameters ####
The Cache Simulator can be configured with the following cache design parameters which are given as command-line arguments:

- number of sets in the cache
- number of blocks in each set
- number of bytes in each block
- write-allocate or not write-allocate
- write-through or write-back
- least-recently-used (LRU) or first-in-first-out (FIFO) evictions

Note that the number of sets in the cache, and the number of blocks per set must be positive powers of 2 for a cache to
"make sense". Furthermore, the size of each block must be a power of 2, with at least 4 bytes.

Write allocate, write through, and LRU will be input into the cache simulator as command-line arguments of 1, while not
write allocate, write back, and FIFO will be input into the cache simulator as command-line arguments of 0. More details
are provided on running the cache simulator in the following section.

#### Running the Cache Simulator ####
``` python csim.py <sets> <blocks> <bytes> <write-allocate> <write-through> <lru> <filename> ```

For example,
``` python csim.py 256 4 16 1 0 1 small.trace ``` will simulate a cache with 4-way associative cache with 256 total sets and
16 bytes per block. This cache will be configured with write-allocate, write-back, and LRU-evictions settings.

#### Output ####
The output after running the above example should be of the following.
```
Total loads: 15
Total stores: 7
Load hits: 8
Load misses: 7
Store hits: 2
Store misses: 5
Total cycles: 4822
```
