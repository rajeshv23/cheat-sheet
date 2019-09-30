
* [commands](https://redis.io/commands)
* [data types](https://redis.io/topics/data-types-intro)
* [REdis Serialization Protocol - RESP](https://redis.io/topics/protocol)  

## Key Spaces ( any binary represenation up to 512 Mb )
* Flat key space
* No automatic namespacing
* Logical Databases ( Database zero )
* Naming conventions ( case sensitive, example user:{unique id of user}:followers

## getting a list of existings keys
![keys list](https://i.postimg.cc/5ygnVyrt/redis-search-key-scan.png)
* keys
```redis
KEYS customer:15*
KEYS cus:15*
KEYS *
```
* scan
```
SCAN 0 MATCH customer*
SCAN 0
```
## retrieve values by key, save collection
```redis
TYPE <key>
OBJECT ENCODING <key>
```
* if value is of type string -> GET <key>
* if value is of type hash -> HGETALL <key>
* if value is of type lists -> 
  * LRANGE <key> <start> <end> ( hgetall )
* if value is of type sets -> 
  * SMEMBERS <key>
* if value is of type sorted sets -> ZRANGEBYSCORE <key> <min> <max>

## insert values, add value
* existence of keys
```
EXIST {key}
# EXIST customer:1500
```

* set value
```redis
# insert only if the record still Not eXists
SET customer:3000 Vitalii NX

# insert only if the record EXXists
SET customer:3000 cherkavi XX
```

## list (always ordered ) operations
  * LLEN
  * LRANGE <key> <start> <end> ( hgetall )
    ```LRANGE my-list 0 -1```
  * LINDEX ( get from specific position )
  * LPUSH ( left push )
  * RPUSH ( right push )
  * LSET 
  * LINSERT ( insert after certain element )
  * LPOP ( left pop )
  * RPOP ( right pop )
  * LREM ( remove element by value )
  * LTRIM ( remove to certain lenght )

## set ( unordered )
  * SADD  
  * SMEMBERS <key>
  * SISMEMBER <key> <value> ( check if value present into set )
  * SCARD ( SSCAN )
  * SREM ( remove by value )
  * SPOP ( pop random!!! element  )
  * SUNION (sql:union), SINTER (sql:inner join), SDIFF ( not in )


## hash value, set value, read hash value
> hash has only one level, can't be embeddable
```
HSET <key> <field1> <value1> <field2> <value2>
HGET <key> <field...>
HMGET <key> <field1> <field2>
HGETALL <key>
```

## increase value
```redis
INCR <key> # for integer
# SET my-personal-key 10
# SET my-personal-key "10"
# INCR my-personal-key
# INCRBY my-personal-key 3
# INCRBYFLOAT my-personal-key 2.5
```

## expiration for key
```
EXPIRE {key} {seconds}
PEXPIRE {key} {miliseconds}

EXPIREAT {key} {timestamp}
PEXPIREAT {key} {miliseconds-timestamp}
```
check expiration, check TimeToLive
```
TTL {key}
```
check living time
```
OBJECT IDLETIME <key>
```
remove expiration
```
PERSIST {key]
```
set with TTL
```
# miliseconds
SET customer:3000 warior PX 60000
# seconds
SET customer:3000 warior EX 60
```

## moving members, cut/paste members
```
SMOVE "source set" "destination set" "member name"
```

## delete 
```
# delete key and value with blocking until removing associated memory block
DEL {key}

# delete key without blocking
UNLINK {key}
```



![client architecture](https://i.postimg.cc/fTp83WSJ/redis-client.png)  
[clients libraries](https://redis.io/clients)  
![connection types](https://i.postimg.cc/rw7qqyR8/redis-deployment-connections.png)  
![redis-java types](https://i.postimg.cc/c4qj1KXk/redis-java-types.png)  
