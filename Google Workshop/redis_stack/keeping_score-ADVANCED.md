## Keeping Score with Sorted sets

Increment a score for the appropriate entry in a SortedSet key:
ZINCRBY <keyname> <score-increase> <unique-participant>
```redis Try it out:
ZINCRBY RedisWorkshopLabs-Z 10 kamlesh.gokal@redis.com
ZINCRBY RedisWorkshopLabs-Z 20 michael.gnesin@redis.com
ZINCRBY RedisWorkshopLabs-Z 30 richard.hanna@redis.com
```

Anytime it is needed, fetch the score for a unique-participant:
```redis 
ZSCORE RedisWorkshopLabs-Z kamlesh.gokal@redis.com
```

Fetch the 5 highest scores and entries by using:
```redis 
ZREVRANGEBYSCORE RedisWorkshopLabs-Z +inf 0 WITHSCORES LIMIT 0 5  
```

## Keeping Score with BloomFilters

Reserve a TOPK key with the expected interesting TOP X results

```redis Try it out:
TOPK.RESERVE RedisWorkshopLab-BF 100 20000 7 0.925
```

Increment an entry for X points scored by a runner in a TopK key:

```redis Try it out:
TOPK.INCRBY RedisWorkshopLab-BF kamlesh.gokal@redis.com 40
```

Check if the score for a unique-participant is within the TOP X results:

```redis Try it out:
TOPK.QUERY RedisWorkshopLab-BF kamlesh.gokal@redis.com
```

Fetch the X highest scores and entries by using:

```redis Try it out:
TOPK.LIST RedisWorkshopLab-BF WITHCOUNT 
```