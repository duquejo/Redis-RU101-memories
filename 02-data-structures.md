<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Introduction to data types

Redis is a data structure server. At its core, Redis provides a collection of native data types that help you solve a wide variety of problems, from caching to queuing to event processing. Below is a short description of each data type, with links to broader overviews and command references.

## Strings
Redis strings are the most basic Redis data type, representing a sequence of bytes.

## Lists
Redis lists are lists of strings sorted by insertion order.

## Sets
Redis sets are unordered collections of unique strings that act like the sets from your favorite programming language (for example, Java HashSets, Python sets, and so on). With a Redis set, you can add, remove, and test for existence in O(1) time (in other words, regardless of the number of set elements).

## Hashes
Redis hashes are record types modeled as collections of field-value pairs. As such, Redis hashes resemble Python dictionaries, Java HashMaps, and Ruby hashes.

## Sorted sets
Redis sorted sets are collections of unique strings that maintain order by each string's associated score.

## Streams
A Redis stream is a data structure that acts like an append-only log. Streams help record events in the order they occur and then syndicate them for processing.

## Geospatial indexes
Redis geospatial indexes are useful for finding locations within a given geographic radius or bounding box.

## Bitmaps
Redis bitmaps let you perform bitwise operations on strings.

## Bitfields
Redis bitfields efficiently encode multiple counters in a string value. Bitfields provide atomic get, set, and increment operations and support different overflow policies.

## HyperLogLog
The Redis HyperLogLog data structures provide probabilistic estimates of the cardinality (i.e., number of elements) of large sets.

Taken from: https://redis.io/docs/data-types/
