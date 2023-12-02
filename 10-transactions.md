<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Transactions

Every transaction has a processing time that has to be concluded to enqueue another one.

Transaction encapsulate one or more Commands

If connections is lost, Redis waits for reconnection and It doesn’t execute anything before connection is restablished. (ALL OR NONE).

Nested transactions are not Supported, but supplied through queues.

### TRANSACTION GENERAL COMMANDS

- MULTI: `MULTI` indicates the start of a Transaction. Queues commands but it doesn’t executes it. Every queue change isn’t applied before execution.
    - MULTI cannot handle nested transactions, it needs to resolve the active one first.
- EXEC: `EXEC` Executes the queued commands. Applies changes for every connected client
    - It EXEC fails, it will return a **(nil)**
- DISCARD: `DISCARD` throws enqueued commands.

The executed commands would return the following results.

- Programming errors:
    - Syntax (wrong parameters): INVALID
    - Operation on incorrect data type: Continue subsequent queued commands but marks as an error.
- System errors
    - Out of memory: Redis tries to resolve each System problems before execute a queue.

Redis transactions has NOT ROLLBACKS, that’s for performance issues avoiding (Penalty). 

## Optimistic Concurrency Control
Observe changes in one or more keys, abort transaction of something changed.

### CONCURRENCY CONTROL COMMANDS

- WATCH: `WATCH key [key ...]` declares interest in one or more keys. if EXEC is applied, it will fail if any of the observed keys are modified.
    - **It has to be called BEFORE the transaction is started.**
    - Multiple WATCH commands can be added before the MULTI.
    - **They are LOCAL to CLIENT and CONNECTION. They are not GLOBAL**
    - All keys are unwatched after EXEC Call automatically
- UNWATCH: `UNWATCH` removes ALL the settted WATCH keys.
