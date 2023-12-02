<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Keys & Expiration (TTL)

## Keys & Expiration

Properties:

- unique
- Binary Safe: Ex “foo”, 42, 3.1415, 0xff
- Key names max size 512MB. (besides long keys not recommended)
- Flat key spaces
- No automatic namespacing (No collections, no databases to group them).
- Logical database is identified by a zero-based index. (Database 0) - Redis Cluster is the only that supports Database Zero

### **Keys naming convention**

user:id:followers, ex: **“user:1000:followers”**

- user: Object name
- 1000: **Unique** identifier of the instance
- followers: Composed object.

Try always have a consistent key naming convention, for conflict avoiding.

They’re case sensitive: Ex: “registeredusers:1000:followers”, “RegisteredUsers:1000:followers”, “registeredUsers:1000:followers”, that’s because the server is doing a binary comparison between each key.

### General commands

- **SET**: `SET key value [EX seconds]` stores a value from a given key.
    - Additional parameters:
        - `[PX milliseconds] [NX|XX]`
            - **NX**: Checks for the non-existence.
                - Ex: `set inventory:100-meters-womens-final 1000 NX` if it doesn’t exists, returns OK or (nil) if exists.
            - **XX**: Checks for the existence.
                - Ex: `set inventory:100-meters-womens-final 0 XX` if exists, updates the value and returns OK or (nil)
- **GET**: `GET key` returns the value from a given key.

Redis always replies each command with a “OK” response (SET).

For a GET request, Redis always returns double quotes for a string variable. Ex. “fred”  

- For iterations through keys/values, use SCAN or KEYS.
- **KEYS**: Retrieves complete blocks of information, so it can keep busy the database for a long time (TAKE CARE). **NEVER USE IN PRODUCTION.** it is SO useful for local debugging.
    - `keys [key pattern]` Ex: `keys customer:1*` retrieves all coincident keys with the prefix and the wildcard (optional).
- **SCAN**: It makes also blocks like KEYS, but it iterates through a cursor, using an iterator pattern. May return 0 or more keys per call. **SAFE FOR PRODUCTION.**
    - `SCAN slot [MATCH pattern] [COUNT count]`
    - Ex: `scan 0 MATCH customer:1*` → 1) “14336” 2) (empty list or set)
    - Ex2: `scan 14336 MATCH customer:1*` → 1) “14848” 2) (empty list or set).
    - Ex3: `scan 1229 MATCH customer:1* COUNT 10000`
    - It can iterate over the results, that could be use as an argument for the next SCAN command.
- **DEL**: `DEL key [key ...]` Removes the key and the associated memory space of it. It **performs a BLOCKING operation.**
    - UNLINK: `UNLINK key [key ...]` The key is unlinked and its removed from memory but the data is reclaimed by an asynchoronous process later. **NON-BLOCKING.**
        - EX: `unlink customer:1000` returns the count of keys associated to the MATCH pattern, if results in zero results, it will return a **(nil).**
- **EXISTS**: `EXISTS key [key ...]` performs a search for a determinated key. It’s recomendable to check first the key before using **SET**. If the key doesn’t exist. **It will be created anyways.**
- **DBSIZE:** `DBSIZE` returns the total number of keys.

### **Keys TTL (Expiration time)**

A key can be setted with a TTL (Time to live) argument. Redis will keep the key in memory until space is required or forced out by an eviction policy

- Seconds
- Milliseconds
- Unix timestamp

It can be removed anytime.

### TTL Commands

- SET:
    - `EXPIRE key seconds`
    - `EXPIREAT key timestamp`
    - `PEXPIRE key milliseconds`
    - `PEXPIREAT key milliseconds-timestamp`
- EXAMINE:
    - `TTL key` expressed in seconds
    - `PTTL key` expressed in miliseconds
- REMOVE TTL (-1)
    - `PERSIST key`

Examples:

- `set seat-hold Row:A:Seat:4 PX 50000` PX → expressed in milliseconds
- `set seat-hold Row:A:Seat:4 EX 50` EX -> expressed in seconds
- Changing expiration time:
    - `pexpire seat-hold 1` (Changing to 1 ms).
    - `ttl seat-hold` Shows the remaining time to expire.
    - `persist seat-hold` retains the key for an unlimited time. (Sets -1 as value).
