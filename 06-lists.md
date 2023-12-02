<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Lists

Ordered sequence of strings, it could be ordered as stacks (Horizontally) or queues (Vertically). (Java ArrayList, Javascript Array, Python List)

Duplicated elements are allowed.

Elements can be inserted relative to another.

**NO CONCEPT OF NESTING EXISTS HERE, just STRINGS**

**Redis implements lists as a DOUBLE LINKED LIST, not as an ARRAY**

If an existent key is different to LIST type, it cannot use the LISTS commands. It will throw an error.

### List Commands

- **RPUSH:** `RPUSH key value [value ...]` pushes elements at the right side of the list.
- **LPUSH**: `LPUSH key value [value ...]`pushes elements at the left side of the list.
- **LPOP**: `LPOP key`   removes the first element from left side in list.
- **RPOP**: `RPOP key`  removes the first element from right side in list.
- **LRANGE:** `LRANGE key start stop` returns a ranged selection from a list, it needs an initial index and a final one, use -1 in “stop” if we want to stop at the end of the list.
- **LLEN:** `LLEN key` checks the list items length count.
- **LINDEX**: `LINDEX key index` retrieves the element at the specified index
- **LINSERT:** `LINSERT key BEFORE | AFTER pivot value` adds an element before or after another element.
- **LSET:** `LSET key index value` sets the value of the specified index.
- **LREM:** `LREM key count value` removes a given number of elements with the specified value.
- **LTRIM**: `LTRIM key start end` prunes the list removing elements on the right.

### Use Cases

- Most recent activity (activty Steam)
- Inter process communication (Producer-consumer pattern)
    - **Producer**:
        - `RPUSH queue “event1”`
    - **Consumer:**
        - `LPOP queue`

**Performance**

LPUSH, RPUSH, LLEN are all o(1) constant time complexity operations

LRANGE o(s+n) is more complex, depends of the number of the elements to retrieve (long lists warning).

**A single list can hold over 4 BILLION ENTRIES:**

**Lists commands differences** 

| Stack |
| --- |
| 0) foo |
| 1) bar |
| 2) baz |

for STACKS use LPUSH and LPOP for values managing.

| Queue | 0) foo | 1) bar | 2) baz |
| --- | --- | --- | --- |

for QUEUES use RPUSH and LPOP for values managing.
