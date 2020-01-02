# Redis

* Redis is not a plain key-value store but in-memory data structure store

**meaning** -  Traditional key-value stores string key associate to string value. In Redis the value can be complex data structures

# Redis Datastructures

## String

```
> set mykey somevalue
OK
> get mykey
"somevalue"
```

### String commands

**SET** - Create/Replace value

String supports atomic increment (Atomic meaning no race condition on same key)


```
> set counter 100
OK
> incr counter
(integer) 101
> incrby counter 50
(integer) 152
```

**GETSET** - Sets a key to a new value, returning the old value as the result
**MSET & MGET** - Multiple key get and set in one command

```
> mset a 10 b 20 c 30
OK
> mget a b c
1) "10"
2) "20"
3) "30"
```

Other commands
* EXISTS, DEL, TYPE, PERSIST, EXPIRE, TTL, PEXPIRE, PTTL

## References:

http://oldblog.antirez.com/post/redis-persistence-demystified.html

https://www.slideshare.net/tim.lossen.de/redis-memory-as-the-new-disk/21-implementation_10k_lines_of_pure

https://riptutorial.com/redis/topic/1724/getting-started-with-redis
