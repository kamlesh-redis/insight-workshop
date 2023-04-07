## Lets implement a rate-limiter
Lets first store the script in LUA ...

```redis Load the script
SCRIPT LOAD "local glimit = 0+ARGV[2] local climit = 0+ARGV[3] local t = (redis.call('TIME')) redis.call('ZREMRANGEBYSCORE',KEYS[1],'0',(t[1]-ARGV[1])) local rcount = (redis.call('ZCARD',KEYS[1])) if (rcount == glimit) then return 'RESOURCE OVERLIMIT:'..redis.call('ZCARD',KEYS[1]) elseif (((redis.call('ZREMRANGEBYSCORE',KEYS[2],'0',(t[1]-ARGV[1]))) < 1000000) and (redis.call('ZCARD',KEYS[2]) < climit)) then return 'Adding '..(redis.call('ZADD',KEYS[2],t[1],t[1]..':'..t[2]))..' point to your count and '..(redis.call('ZADD',KEYS[1],t[1],t[1]..':'..t[2]))..' point to the resource count' else return KEYS[2]..' CONSUMER OVERLIMIT: '..redis.call('ZCARD',KEYS[2]) end"
```

This will return a SHA-Value uniquely identifying this script for execution.
Go ahead and copy it now

You will pass some parameters along with that SHA-value to execute the script.

```redis for example...
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
```

The above command is doing the following:
- 2 = number of redis KEYS that will be passed in ( a neccessary part of using Lua with redis)
- ratelimit:global:calc{a} == shared resource key
- ratelimit:consumer6:calc{a} == consumer for resource key
- 10 == time window to govern measured in seconds
- 5 == size of allowed operations count for shared resource key
- 3 == size of allowed operations count for consumer for resource key

Now if you execute this command several times, when the consumer limit is reached you will get an error message.

```redis Lets see it in action
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
EVALSHA <replace-me> 2 ratelimit:global:calc{a} ratelimit:consumer6:calc{a} 10 5 3
```

You should see that the 4th call hit the api-limit for a consumer...

You can learn more here: https://github.com/owentechnologist/LUA_rateLimiting

