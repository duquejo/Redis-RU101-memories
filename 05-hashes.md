<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# hashes (key/value pairs)

They’ve like JSON objects structure, Java Hashmap or Python dictionary.

They are mutable (add, change, increment, remove) but they have Flat values. (No nested values).

### Hashes Commands

- **HSET**: `HSET key` this structure depends of the positions of the key separated by colons.
    - Ex: `HSET player:42 name Artexius race Elf level 4 hp 20 gold 20`
    - **HMSET**: has the SAME function as HSET (As per Redis 4.0.0).
- HLEN: `HLEN key` returns the length or cardinality of the hash.
- **HGETALL**: `HGETALL key` returns all the existing key-value indexes for the given key.
- **HSET:** `HSET player:42 status dazed` updates the hash key adding a new key-value pair.
- **HSETNX:** `HSETNX key field value` Sets a value in a HASH only if the field does not already exist.
- **HDEL:** `HDEL player:42 status` removes the entire key-value pair by its inner key.
- **HINCRBY:** `HINCRBY player:42 gold 120` executes a INCRBY operation over a specified key.
    - **There is not a command for DECREMENT, so, HINCRBY could be sent with a negative number.**
- **HINCRBYFLOAT:** `HINCRBYFLOAT key field increment` executes a INCRBYFLOAT operation.
- **HGET**: `HGET key field` retrieves the value from the given key and field, returns (nil) if doesn’t exists. The command can be called even if the field does not exist.
- **HSCAN:** `HSCAN key cursor [MATCH pattern] [COUNT count]`  iterates over fields matching the supplied pattern.
- **HMGET**: `HMGET key field1 field2` retrieves all the specified fields from a given key.
- **HEXISTS**: `HEXISTS key field` is used for check a field from a given key. (1 yes - 0 no)
- **HKEYS**: `HKEYS key` retrieves all the key names
- **HVALS**: `HVALS key` retrieves all the key values

**HGET, HSET, HINCRBY, HDEL, hash operations are performed over a o(1) constant amount of time regardless the size of the hash. THEY are super efficient.**

HGETALL has a **o(n) variable amount of processing time. Is dependent on how many fields it has to retrieve. For large amount of fields in a hash is usually most efficient to select the exact fields using HMGET**

### Use Cases

- **Rate limiting:** Ex: `HMSET rate-endpoint “/pet/{petID}” 100 “/booking/{petId}” 100` depends of the dynamic value modification.
    - `HINCRBY rate-endpoint "/pet/{petId}" -1` reduce the rate for each time the API call is made.
    - `EXPIRE rate-endpoint 86400` sets the TTL for the quota limiter dynamically.
- **Session Cache: Ex: `HMSET session`**

**REDIS JSON is a Redis module which is capable to handle NESTED structures and it has all the commands to GET; update, delete, and more.**
