<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Redis Introduction *

If you’re familiar with relational databases, you’ll no doubt have written SQL queries to relate data between tables. Redis is a type of database that’s commonly referred to as No SQL or non-relational. In Redis, there are no tables, and there’s no database-defined or -enforced way of relating data in Redis with other data in Redis.

It’s not uncommon to hear Redis compared to memcached, which is a very high-performance, key-value cache server. Like memcached, Redis can also store a mapping of keys to values and can even achieve similar performance levels as memcached. But the similarities end quickly — Redis supports the writing of its data to disk automatically in two different ways, and can store data in four structures in addition to plain string keys as memcached does. These and other differences allow Redis to solve a wider range of problems, and allow Redis to be used either as a primary database or as an auxiliary database with other storage systems.

## Benchmark
| Name | Type	| Data storage options | Query types	| Additional features |
|---|---|---|---|---|
|Redis|	In-memory non-relational database |	Strings, lists, sets, hashes, sorted sets, bitmaps, geospatial	| Commands for each data type for common access patterns, with bulk operations, and partial transaction support	| Publish/Subscribe, master/slave replication, disk persistence, scripting (stored procedures) |
| memcached	| In-memory key-value cache	| Mapping of keys to values |	Commands for create, read, update, delete, and a few others	| Multithreaded server for additional performance |
| MySQL	| Relational database |	Databases of tables of rows, views over tables, spatial and third-party extensions	| SELECT, INSERT, UPDATE, DELETE, functions, stored procedures | ACID compliant (with InnoDB), master/slave and master/master replication |
| PostgreSQL | Relational database | Databases of tables of rows, views over tables, spatial and third-party extensions, customizable types	| SELECT, INSERT, UPDATE, DELETE, built-in functions, custom stored procedures |	ACID compliant, master/slave replication, multi-master replication (third party) |
| MongoDB	| On-disk non-relational document store |	Databases of tables of schema-less BSON documents	| Commands for create, read, update, delete, conditional queries, and more |	Supports map-reduce operations, master/slave replication, sharding, spatial indexes |

Taken from: https://redis.com/ebook/part-1-getting-started/chapter-1-getting-to-know-redis/1-1-what-is-redis/1-1-1-redis-compared-to-other-databases-and-software/

## Use Cases
- Inventory control
- State management
- Seat reservations
- Notifications
- etc..

Redis has a trial/paid cloud service, Redis Cloud: AWS, GCP, Azure.
