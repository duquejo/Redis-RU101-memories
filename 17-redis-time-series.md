<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Redis Time Series

## Redis Time Series
- Data Ingestion module with low latency which is often used in general statistics.
- It’s a Tuple, TImestamp plus a measurement (floating point value). (known as sample).
- Supports cleanup of old samples with max retention settings.
- Supports range queries
- Supports aggregations: average, max, min, etc.
- It must be loaded module into Redis.

A RedisTimeSeries structure isn't a set, so the values you enter don't have to be unique. With sorted set sets, we had to make each recorded value unique by appending the minute value to it.

### Use Cases:
- Finance and stock market analysis
- Real-time device monitoring and factory production tracking.
- Historical data analysis

### RTS Commands

- **TS.CREATE**: `TS.CREATE key RETENTION ms CHUNK_SIZE kb DUPLICATE_POLICY [MAX|BLOCK|LAST|SUM] LABELS [... labels]`   Chunk_Size default 4096 kb. Duplicate policy allows different case uses for duplicate values handling.
    - `LAST` replaces the sample with the newest reading.
- **TS.ADD** `TS.ADD key [*|ms] measurement RETENTION retentionInMs`   * is for delegate Redis timestamp based on a Redis Server System Clock. Instantiates a new time series. Returns the specified ms.
- **TS.ALTER** `TS.ALTER key RETENTION ms CHUNK_SIZE kb DUPLICATE_POLICY [MAX|BLOCK|LAST|SUM] LABELS [... labels]` Updates the initial TS.CREATE config for a given key.
- **TS.RANGE** `TS.RANGE start stop FILTER_BY_VALUE min max AGGREGATION [SUM|MAX|MIN|AVG] value`       Gets all registries in the specified interval
    - Aggregation enables adding more statistics to the results.
    - Returns the samples as an array of arrays. `Timestamp & value as string
- **TS.REVRANGE**: `TS.REVRANGE key`  allows return results like `TS.RANGE` but given in reverse order (Recent to oldest).
- **TS.CREATERULE**: Adds timestamps and samples from a one-time series to a second-time series.
- **TS.QUERYINDEX**: Queries across all the time series between labels and keys, or label to more than 1 label, etc. (=, !=, label = (label1, label2, ...), etc...)
