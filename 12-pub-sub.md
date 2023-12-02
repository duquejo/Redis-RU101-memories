<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Pub/Sub

Redis could act as a broker.
Redis couldn’t guarantee that a recently sent message is sent to a recently connected subscriber. It needs to be connected before the message is sent.
Messages conception is “FIRE-AND-FORGET”.

## Case uses:
- Fan Out
    - Analytics
        - Sales by event
        - Sales by time of day
    - Notifier
        - Pick lottery winners
        - Show real time orders

### ADMIN PUB/SUB COMMANDS:

- PUBSUB: `PUBSUB subcommand [args [args…]]`` allows for introspection of the publish
    - CHANNELS: `PUBSUB CHANNELS [pattern]` list of active channels.
    - NUMSUB: `PUBSUB NUMSUB [channel-1 ... channel-N]` returns the number of subscribers excluding patterned subscribers.
    - NUMPAT: `PUBSUB NUMPAT` returns the number of the patterned subscribers.

### SIMPLE SYNDICATION COMMANDS:

- PUBLISH `PUBLISH channel message`pushes a new message to the channel
- SUBSCRIBE `SUBSCRIBE channel [channel ...]` subscribes to one or more channels
    - SUBSCRIBE is a blocking command. But can accept other comamnds, as UNSUBSCRIBE
    - WHEN IS EXECUTED FOR THE FIRST TIME: Returns the applied command, the channel and the active subscribers **that this client has.**
    - WHEN RECEIVES A MESSAGE: Returns the message string (indication), the channel and the value of the sent message.
- UNSUBSCRIBE: `UNSUBSCRIBE [channel [ channel …]]` stop listening messages on a channel.
- Admin
  - PUBSUB: `PUBSUB subcommand [args [args…]]`` allows for introspection of the publish
