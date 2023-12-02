<p align="center"><a href="https://university.redis.com" target="_blank"><img src="https://prod-amc-bucket.s3.amazonaws.com/customer_files/2_redis-university-reversedRGB.png" alt="Redis University" /></a></p>
<p align="center">Redis Developer Certification Walkthrough notes</p>

# Geospatial

Indexes a key value that is built by a pair of values (latitude and longitude), and an unique name. A Geospatial value has a GeoHash data type, is a 52bit integer value in redis. Gustavo Niemeyer created this convention. **The SORTED SET is the data type for explain Geospatial objects so it can use all SORTED SET commands.**

Take care with `ZINTERSTORE AGGREGATE MIN`and `ZUNIONSTORE AGGREGATE MIN` because the points should not change. Adding MIN/MAX aggregate operator it will retain the values.

For Remove Geospatial objects, use `ZREM`.

The Geospatial data structure are based on the Haversine formula, Redis calculations are more precise when the points are closer to the Equator. For more farthest locations, the accuracy decreases by 0.5%

**Valid longitudes are from -180 to 180 degrees.**

**Valid latitudes are from -85.05112878 to 85.05112878 degrees.**

### Use Cases:

Related to located general questions:

- What are the five nearest X locations to my current location?
- How far is it from here to X?
- List locations within a given radius

### GEOSPATIAL COMMANDS:

- GEOADD: `GEOADD key lng lat member`
    - It supports multiple coords concatenation like: `GEOADD key lng lat member [lng lat name ...]`
- GEORADIUS: `GEORADIUS key centerlng centerlat radius m|km|ft|mi [WITHDIST|WITHCOORDS] [COUNT number]` returns all the Geolocations names that are close to the center coordinates.
    - BY DEFAULT GEORADIUS returns coordinates in an unsorted order.
    - GEORADIUS can also retrieve all the distances from the provided center to the other locations with `GEORADIUS key centerlng centerlat radius m|km|ft|mi WITHDIST` that returns all the close geolocation coords with its distance.
    - GEORADIUS cal also retrieve all the coordinates from the provided center to the other locations with `GEORADIUS key centerlng centerlat radius m|km|ft|mi WITHCOORDS` option.
        
        WITHHASH also exists too.
        
    - You can retrieve the locations ordered using at the end the `ASC` option. (Nearest to Farthest), from the Farthest to Nearest use `DESC` option.
    - You can limit the number of the search results with `COUNT number` option.
    - You can STORE the results in another variable with the `STORE|STOREDIST key`.
- GEORADIUSBYMEMBER: `GEORADIUSBYMEMBER key member radius m|km|ft|mi [WITHCOORD][WITHDIST][WITHHASH] [Count count] [ASC|DESC] [STORE key] [STOREDIST key]` isused to retrieve all the members close to the center member.
    - You can STORE the results in another variable with the `STORE|STOREDIST key`.
- ZRANGE: `ZRANGE key start end WITHSCORES` could retrieve all data from a Geospatial object, it returns the lng and lat (y,x) as a 52bit Integer
- GEOHASH: `GEOHASH key member [member ...]` returns the GeoHash for one o more members of the set.
    - Returns an 11 character representation of the hashed value. That’s a structure used for many sustems and services, for example: *geohash.org*. For shorten hash range, is less precise the coordinates for the member point.
- GEOPOS: `GEOPOS key member [member ...]` returns the longitude and latitude for one o more members.
- GEODIST: `GEODIST key member1 member2 [unit]`Retrieve the distance between two members with the same key
    - UNIT can be return the distance in meters, kilometers feet and miles.
    - **IT CANNOT WORK ACROSS TWO DIFFERENT KEYS**
