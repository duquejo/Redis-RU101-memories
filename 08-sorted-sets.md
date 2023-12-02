<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Sorted Sets

### **Sorted Sets**

Ordered collection of unique string members. The Sorting order is given by a floating-point SCORE value.

It can be manipulated by VALUE, POSITION, SCORE or LEXIGRAPHICALLY.

Can perform DIFF, UNION and INTERSECTION.

NESTING, HASHES, LISTS, etc.. are NOT ALLOWED.

**SORTED SETS can have duplicated SCORES but not the same VALUES, that’s because Redis performs a LEXIGRAPHICALLY comparison between them. So If you executes a `ZRANGE` command, it will return the alphabetic order between values excluding duplicated scores.**

Use Cases

- Priority queues
- Low-latency leaderboards
- secondary indexing

### SORTED SETS COMMANDS

- ZADD: `ZADD key [NX|XX] [CH] [INCR] SCORE MEMBER [SCORE MEMBER ...]` NX Only adds new elements of the value does not already exist. XX only updates an existing element. returns the number of the elements added. Ex: `ZADD subway 1 Tokyo` `ZADD subway 5 "Shin-Kiba" 3 "Etchujima" 2 "Hatchobori"`
- ZINCRBY `ZINCRBY key increment member` Adds the increment value to the current member SCORE.
- ZCARD `ZCARD key` retrieves the total number of elements in the SORTED SET.
- ZDESCBR
- ZRANGE `ZRANGE key start stop [WITHSCORES]` get elements from a SET, from the lowest score to the hightest index ASCENDING.
- ZREVRANGE `ZREVRANGE key start end [WITHSCORES`] get elements from a SET, from the highest score to the lowest score (index) DESCENDING.
- ZRANGEBYSCORE: `ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]`
- ZRANGEBYLEX: `ZRANGEBYLEX key min max [LIMIT offset count]`
- ZRANK: `ZRANK key member` Gets the member INDEX (0 to -1) from a SORTED set.
- ZREVRANK: `ZREVRANK key member` Gets score rank (index) from a SORTED set.
- ZSCORE: `ZSCORE key member` Returns the score of the specified member value.
- ZCOUNT: `ZCOUNT key min max` Counts the number of elements between a range of SCORES.
- ZREM: `ZREM key value [value ...]` removes one or more element VALUES from a SET.
- ZREMRANGEBYLEX: Lexicographically
- ZREMRANGEBYRANK: Position (index)
- ZRAMRANGEBYSCORE: Score
- ZINTERSTORE: `ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight]] [AGGREGATE SUM|MIN|MAX]`
- ZUNIONSTORE: `ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weight [weight]] [AGGREGATE SUM|MIN|MAX]`
- ZDIFFSTORE: `ZDIFFSTORE destination numkeys key [key ...]`
