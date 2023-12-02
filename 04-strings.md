<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Strings

Binary safe sequences of bytes (integers, floating point numbers, binary values, comma-separated values, serialized JSON, objects, images, videos, etc). Maximum 512 MB.

### Common Uses

- Caching
- Session storage
- HTML pages
- Counters (Increment/Decrement).

### String Commands

- **INCR**: `INCR user:23:visit-count` creates a new key with the value of 1 if doesn’t exist yet.
- **INCRBY**: `INCRBY user:23:credit-balance 30` creates a new key / or updates its value adding 30 as integer value.
    - Also supports negative numbers like: `INCRBY user:23:credit-balance -50` disminishes the current value by 50.
- **DECBRY**: `DECRBY key decrement` for diminish by the setted value.
- **DECR**: `DECR key` for diminish by 1.
- **INCRBYFLOAT**: `INCRBYFLOAT key increment` for float point numbers manipulation
- **TYPE**: `TYPE key` returns the data type of the key.
- **OBJECT:** `OBJECT encoding key` for key encoding type check use:  it will return the native value, ex: “int”, “embstr” (text), etc…

**If the current value is actually has a STRING NUMBER format and you apply INCR/DECR command, it will work, but transforming and updating the value as INTEGER.**

**INCR/DECR commands ONLY operates on values encoded as integers**
