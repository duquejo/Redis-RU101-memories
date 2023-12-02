<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Sets

Unordered collections list of strings that contains no duplicates: {3,1,5}. Is not guaranteed an specific items order. If you need any order, use **SORTED SETS data structure.**

**Works only with the STRING datatype, nested LIST, SET, SORTED SET or HASH are not allowed, and only works with flat strings.**

SETS works too with **EXPIRE, so you can configure a TTL for a specific number of seconds. ALL ELEMENTS are deleted when EXPIRE is setted.**

**Time-scoped key expiration strategy definition:**

![Untitled](/sort-strategy.png)

### Use Cases

- Did I see this IP in the last hour?.
- Is this user online?.
- Has this URL been blacklisted?.
- Tag clouds
- Unique visitors

Operations used for key configuration: Intersection, Difference, Union.

### SETS COMMANDS

- **SADD**: `SADD players:online 42`  returns number of elements added.
- **SCARD**: `SCARD players:online` retrieves the total number of items added in the SET collection as a integer.
- **SISMEMBER**: `SISMEMBER players:online 42` checks if the provided value exists already in the SET collection. (1 if exists, 0 if doesn’t exists).
- **SMEMBERS**: `SMEMBERS key` retrieves all elements of a SET (BLOCKING-OPERATION)
- **SSCAN**: `SSCAN key cursor [MATCH pattern] [COUNT count]` retrieve elements based on a cursor.
- **SREM**: `SREM key member [member ...]` removes one or more elements by a given value, returns 1 if exists.
- **SPOP**: `SPOP key [count]` will remove and RETURN a (or many) random elements from the SET.
- **SUNION**: `SUNION key1 key2` will perform the UNION returning all the unique values.
- **SDIFF**: `SDIFF key1 key2` will return the difference from the FIRST SET with the subsequent SETS given.
- **SINTER**: `SINTER player:31:friends players:online` performs a intersection between two given SET collections.
