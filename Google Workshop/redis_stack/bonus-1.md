## Bonus Questions:
Now the answers are only a click-away, try to use autocomplete to figure it out first.

1) How do you check the remaining time for a key set to expire?
```redis Click here to see the answer.
SET key value
EXPIRE key 10
TTL key
```
2) How many keys are there currently in Redis? (e.g. info)?
```redis Click here to see the answer.
DBSIZE
```

3) How to you remove all the keys in the keyspace?
```redis Click here to see the answer.
FLUSHDB
FLUSHALL
```

4) What is the difference between DEL and UNLINK?
```redis Click here to see the answer.
DEL blocks all commands until complete,
UNLINK doesnt block commands, and deletes using another thread.
```

5) Get just fields,  just the values or all of the fields and values in the hashkey 

```redis Click here to see the answer.
HMSET myHash 1 1 2 2 3 3
HKEYS myHash
HVALS myHash
```