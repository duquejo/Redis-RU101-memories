<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Bitmaps

It’s like a array of bits stored in a String, Supports Bitfields & Bitarrays
For a BITFIELD the object encoding is **RAW**, but the **TYPE** is **STRING**.
Compact, and optimized structures: Histogram of counters, file permissions, 

## USE CASES

- Histograms
- Permission bits & masks
- Seat reservations

**There is not explicit bit data type.**

Operations between Bitmaps:
- AND
- OR
  - ![Untitled](/bitmap_or.png)
- XOR
- NOT

### BITMAPS COMMANDS:

- SETBIT: `SETBIT key offset value`   Sets an individual bit.
- GETBIT: `GETBIT key offset` Gets an individual bit
- BITCOUNT: `BITCOUNT key [start end [BYTE|BIT]`  retrieves the count number of setted bits in the entire string.
- BITOP: `BITOP operation destkey key [key ...]` operation to perform such as AND, OR, EXCLUSIVE OR (XOR) and NOT.

### BITFIELD COMMANDS:

Type: Signed (i), Usigned (u), The size has not importancy, it could be 4,5 or 11, etc…

**Limits: i64 por Signed, and u63 for unsigned**

If the OFFSET is prefixed with a `#`  *(HASH or POUND)* character, the specified offset is MULTIPLIED BY THE INTEGER encoding’s width.

`BITFIELD mystring SET i8 #0 100 SET i8 #1 200`

Will set the first i8 integer at offset 0 and the second at offset 8. 

![Untitled](/bitfield_get.png)

Getting BITFIELD from positional value `#` and the `offset`aprox.

- BITFIELD SET: `BITFIELD key SET encoding offset value` Creates a BITFIELD with the specified args.
    - Ex: `BITFIELD mykey SET u8 0 42` creates a BITMAP key field with an unsigned 8-bit value at bit offset zero to the value 42.
- BITFIELD GET: `BITFIELD key GET encoding offset` retrieves the value stored in the offset value.
    - Ex: `BITFIELD mykey GET u8 0`
- BITFIELD INCREASE: `BITFIELD key INCRBY encoding offset value` Increments a specified value into the given offset.

A bitfield can be indexed by offset and indexed by position

![Untitled](/bitfield_indexes.png)

When a BITFIELD is retrieved with the command GET, the result is given as a Hexagesimal value of the offset representation.
