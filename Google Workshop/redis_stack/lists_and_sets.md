## List Exercises

Create a queue of 5 email addresses 

```redis Try it out:
LPUSH my_queue kamlesh.gokal@redis.com
LPUSH my_queue michael.gnesin@redis.com
LPUSH my_queue lejo.jacob@redis.com
LPUSH my_queue shyam.kathiresan@redis.com
LPUSH my_queue richard.hanna@redis.com

lrange my_queue 0 5
```

Remove the first element off the queue

```redis Try it out:
RPOP my_queue

lrange my_queue 0 4
```

Remove one element from the end of queue and add it to another in one step

```redis Try it out
RPOPLPUSH my_queue my_other_queue

lrange my_queue 0 5
lrange my_other_queue 0 1
```

## Sorted Set Exercises

Add the stooges
```redis Try it out
zadd beststooges 10 Larry 20 Curly 30 Moe 40 Shemp

ZRANGE beststooges 0 6
```

What is the rank of Curly?
```redis Try it out
ZRANK beststooges Curly
```

Can different members be added to a zSet with the same score?
```redis Try it out
zadd beststooges 10 ProfessorJones

ZRANGE beststooges 0 5 WITHSCORES
```

Can you have the same member with different scores?
```redis Try it out
zadd beststooges 1 Moe

ZRANGE beststooges 0 5 WITHSCORES
```

Get 2 lowest scoring stooges
```redis Try it out
ZRANGE beststooges -2 -1
```

Can you create a Union or Intersection between a Sorted Set and Set?
```redis Try it out
SADD stooges Curly Larry Moe FakeShemp ShortyWilliams FullerBull ProfessorJones Dr.LarryFine YoungLarry YoungTeddy SchuylerDavis

ZUNION 2 stooges beststooges

ZINTER 2 stooges beststooges
```
