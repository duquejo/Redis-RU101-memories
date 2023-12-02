<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Lua Scripting

That’s a solution for stored procedures in Redis.
Lua programming language, embedabble scripting language. MIT Open source Project. Reduces network traffic manipulating multiple keys inside a single database procedure

**Redis is a simple threaded system, every transaction is a single atomic unit to process.**

**Lua Arrays are One Indexed - Ex: KEYS[1]**

**A script may run for up to FIVE seconds before Redis starts accepting new commands.**

When a Redis execution threshold has been exceeded, Redis will not terminate the script.

For identify that:

- First: Redis Server logs a message indicating a **long running script.**
- Second: Redis will start accepting new commands but these commands won’t actually be executed, Redis will respond a BUSY response.
- If a script is READ ONLY or the script has surpassed the execution threshold but has not performed a right, then the `SCRIPT KILL` Command can be executed to terminate the Script Safely.
    - If data has been written, then the only option is to execute the `SHUTDOWN NOSAVE` command, indicating a server termination without saving any pending changes.

### Use Cases

- Ensure a set of commands are executed together and avoid some of the complexity of a transaction and optimistic concurrency control.
- Limited Counters
    - Count by period
    - Adjust counter
    - Allow request of threshold not exceeded

### Lua Scripting Commands

- EVAL: `EVAL script numkeys key [key ...] arg [arg ...]`
    - For the script, you can use `redis.call` which after an exception it will simply propagate the error back, causing EVAL to fail.
    - You can use also `redis.pcall` which will return a structure representing the error response.
    - It is a **BLOCKING COMMAND:**
    - Ex:
        - `EVAL "return redis.call('HGET', KEYS[1], ARGV[1])" 1 hash-key field2`
            - For EVAL, KEYS is always returned as a List of n fields number given in the EVAL/numkeys parameter, Similarily for ARGV.
- SCRIPT LOAD: `SCRIPT LOAD script` Eval caches compiled scripts, returns the script hash digest.
- EVALSHA: `EVALSHA sha1 numkeys key [key …] arg [arg …]` invokes the script through hash. **BLOCKING COMMAND.**
- SCRIPT EXISTS: `SCRIPT EXISTS sha1 [sha1 ...]` evaluates if the given hash exists, returns a booleans array.
- SCRIPT FLUSH: `SCRIPT FLUSH` removes all scripts that Redis cached.
- SCRIPT KILL: `SCRIPT KILL` Stops any active EVAL/EVALSHA blocked command.
- SCRIPT DEBUG: `SCRIPT DEBUG YES|SYNC|NO`  invokes an interactive debugger for Lua.
    - **NEVER USE IN PRODUCTION**

### Lua Rules

- Rule #1
    - Keys should be passed in.
    - Keys should not be hard-coded.
- Rule #2
    - Arrays are one-based
- Rule #3
    - **Floats are truncated (Here isn’t differences between Integer and float types).**
        - **Decimal pointers are going to be loosen.**
        - **For preservation, you must to pass numbers as a Strings.**

## Variables translation    
![Untitled](/lua_table.png)

### Basic Lua Syntax
```lua
-- variables
local k1 = redis.call('get', KEYS[1])

-- conditionals
if `condition` then
  return x
else then
  return nil
end

-- operators
-- == equality, <, >, <=, >=, ~=
-- or, and, not
-- false/nil are considered false and anything else true

-- strings concatenation 'string' .. 'string' or variable like KEYS[1]
-- tonumber - to number convertion

-- loops
for _, variable in ipairs(list) do -- ipairs creates an iterator from lua array
  -- something
end
```
