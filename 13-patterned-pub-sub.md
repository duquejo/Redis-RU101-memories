<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Patterned Pub/Sub

Often we have to receive a subset of the all received messages.

### PATTERNED SYNDICATION COMMANDS:

As the number of patterns increases, more work and more latency will be introduced.

- PSUBSCRIBE: `PSUBSCRIBE pattern [pattern …]` allows pattern subscription to limit the messages we receive.
    - Allowed patterns:
        - ? - Single character wildcard
        - * - Multiple characters wildcard
        - […] - alternate characters
        - ^ - Prefixes
            - Ex:
                - h?llo subscribes to hello, hallo and hxllo
                - h*llo subscribes to hllo and heeeello
                - h[ae]llo subscribes to hello and hallo, but not hillo
                - h[^e]llo subscribes to hallo, hbllo, ... but not hello
    - WHEN IS EXECUTED FOR THE FIRST TIME: Returns the command, the pattern match, and the number of clients subscribed with this pattern.
    - WHEN RECEIVES A MESSAGE: Returns the command, the pattern match, the actual channel that the message was sent, and the value.
- PUNSUBSCRIBE: `PUNSUBSCRIBE [pattern [pattern …]]`
