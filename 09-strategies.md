<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Data management strategies

- Redis has not compound indexes and secondary indexes
- Retrieve all the objects (”secondary indexes”)
- Faceted Search
- Hashed Search

More info: https://elwillie.es/2022/10/09/redis-busqueda-de-claves-segun-sus-atributos/

## How to store complex objects

- Multiple hashes
    - Use a hash for each object.
- Multiple hashes + Sets

**Flattening relationship in a single Hash**
This is the most common strategy
![Untitled](/flattening_object.png)

**The available keys can be transformed into:**
- **available:general:qty → 20000**
- **available:general:price → 25.00**

### PROS
- Automic updates/deletes
- No transaction
- Encapsulation **(When the key is deleted ALL the associated hash keys value are removed - LIKE A CASCADE DELETE) on a foreign key.**

### CONS
- Remove all fields at once is hard to maintain.
- Large objects makes hard to iterate and maintain that.

**Multiple hashes**
![Untitled](/multiple_hashes.png)

**Multiple hashes + Sets**
![Untitled](/multiple_hashes_sets.png)

### PROS
- Extensible strcutures
- Independently stored
- Expiration can be applied outside

### CONS
- Too many fields for object representation
- Relationship maintenance
- Cluster
