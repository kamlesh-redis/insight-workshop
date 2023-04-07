In this tutorial, we will go through an example of Strings and Hashes...


## Storing and managing Strings
Lets get and set a string ...

```redis Set a userid:1 key with your name
SET USERID:1 Jane
```

```redis Get the value from the userid:1
GET USERID:1
```

Now lets play with TTL's ...

```redis Expire the value in 10 seconds
EXPIRE USERID:1 10
```

```redis Wait for 10 seconds then try to get the value again 
GET USERID:1
```

You can see Redis returns 'NIL' when a key is not found.
Lets try another way keys can be removed

```redis Set the same userid:1 with a value one more time
SET USERID:1 Jane
```

Sometimes DEL is an expensive command, try using UNLINK ...

```redis Unlink the userid:1
UNLINK USERID:1
```

```redis Try to get the value again
GET USERID:1
```












