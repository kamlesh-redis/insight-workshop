## Track runners scores in a race

## Using Sorted Set
Simulate storing race score totals between 3 runners - Xi, Sally, Amit
Use ZINCRBY to increase scores for the 3 runners in a shared SortedSet called: day{1}:results
Example: 
```redis Try it out:
ZINCRBY day{1}:results 3 Amit
ZINCRBY day{1}:results 3 Sally
ZINCRBY day{1}:results 4 Xi

ZRANGE day{1}:results 0 5 WITHSCORES
```

Once you have modified each runners’ score (the yellow highlighted value) 4 times:
Check the 3 runners scores by using:
```redis Try it out: 
ZREVRANGEBYSCORE day{1}:results +inf 0 WITHSCORES LIMIT 0 3
```

## Using TOPK

Simulate storing race score totals between 3000 runners - Xi_1, Sally_1, Amit_1, …, Amit_1000
Create a Redis  SET called possible:scores{2} that contains 5 Score values:  1, 2, 3, 4, 5  

Reserve a TOPK key that has capacity for the top 10 scores called: day{2}:results

```redis Try it out: 
TOPK.RESERVE results 10 10000 7 0.925
SADD scores 1 2 3 4 5
```

The following script uses SRANDMEMBER to repeatedly and randomly fetch scores & uses TOPK.INCRBY to increase scores for the 3000 runners in the TOPK key: 
Note: LUA SCRIPTS can execute for loops like this: (below we specify 10 races for 1000 unique runners)

```redis Try it out: 
10 EVAL "for index = 1,1000 do redis.call('TOPK.INCRBY',KEYS[1],ARGV[1]..'_'..index, redis.call('SRANDMEMBER',KEYS[2])) end  return 'done'" 2 results scores Amit

10 EVAL "for index = 1,1000 do redis.call('TOPK.INCRBY',KEYS[1],ARGV[1]..'_'..index, redis.call('SRANDMEMBER',KEYS[2])) end  return 'done'" 2 results scores Sally

10 EVAL "for index = 1,1000 do redis.call('TOPK.INCRBY',KEYS[1],ARGV[1]..'_'..index, redis.call('SRANDMEMBER',KEYS[2])) end  return 'done'" 2 results scores Xi
```

Once you have modified each runners’ score 10 times:
Check the top 10 runners’ scores by using:

```redis Try it out: 
TOPK.LIST results WITHCOUNT
```