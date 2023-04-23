## Streams

ADD to stream new-hires and includes the fields name and start-date for yourself
```redis Try it out:
XADD new-hires * name Jane start-date 2020-01-01
```

READ the element of the stream
-- This Command is not supported in RedisInsight, but you can see the syntax.
XREAD STREAMS new-hires 0

READ the first two element of the stream
-- This Command is not supported in RedisInsight, but you can see the syntax.
XREAD COUNT 2 STREAMS new-hires 0-0


Get the elements using XRANGE from oldest to newest
```redis Try it out:
XRANGE new-hires - +
XRANGE new-hires - + COUNT 2
```

Get the elements using XREVRANGE from newest to oldest
```redis Try it out:
XREVRANGE new-hires + -
XREVRANGE new-hires + -  COUNT 2
```

ADD to stream new-hires and includes the fields name and start-date for yourself
/* Rerun this command a few times */
```redis Try it out:
XADD new-hires * name TheSkipper start-date 2020-01-01
XADD new-hires * name Gilligan start-date 2020-01-02
XADD new-hires * name TheProfessor start-date 2020-01-03
XADD new-hires * name MaryAnn start-date 2020-01-04
XADD new-hires * name Tiffany start-date 2020-01-05
XADD new-hires * name Thurston start-date 2020-01-06
XADD new-hires * name Eunice start-date 2020-01-07
```


Get length of new-hires
```redis Try it out:
XLEN new-hires
```

ADD to stream new-hires but limit the number of entries to 20 and then check for length
```redis Try it out:
XADD new-hires MAXLEN 20 * name Skipper start-date 2020-02-01
XLEN new-hires
```

TRIM the stream new-hires  down to approximately 10 entries
```redis Try it out:
XTRIM new-hires MAXLEN ~ 10
XLEN new-hires
XINFO STREAM new-hires
```