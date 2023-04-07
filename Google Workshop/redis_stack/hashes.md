In this tutorial, we will go through an example of Hashes...


## Storing and managing Hashes
Lets start with a basic Hash ...

```redis Set some session data into a hash
HSET usersession:2 userid 123456 firstname Harry lastname Potter ip 127.0.0.1 lastvisit Hogwarts
```

```redis Now lets get all the fields
HGETALL usersession:2
```

You can see Redis returns all data in Key Value pairs...

```redis Increment hits by 1 
HINCRBY usersession:2 hits 1
```
(note that you didn't set a value)

You can also get a subset of fields of the hash

```redis Get userid, firstname and hits 
HMGET usersession:2 userid firstname hits
```

(look at the value of hits)

```redis Set a new ip of 198.1.1.0
HSET usersession:2 ip 198.1.1.0
```

```redis Delete the lastname
HDEL usersession:2 lastname
```

Now that we've done some changes, lets see what it looks like.

```redis Let's see the results
HGETALL usersession:2
```
