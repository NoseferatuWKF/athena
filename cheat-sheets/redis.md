[redis.conf](https://redis.io/docs/latest/operate/oss_and_stack/management/config-file/)

connect to remote
```bash
redis-cli -h <host|ip> -p <port>
```

redis-server
```bash
# configuring default password and user password
redis-server --requirepass password "--user myuser on >mypassword ~* +@all"
```

monitoring
```bash
redis-cli monitor
```

basic operations
```bash
FLUSHALL # remove everything
keys <pattern> # list keys by pattern, key * to get all
get <key> # get values by key
del <key> # remove key(s)
```

operations
```bash
# remove all keys matching pattern 
redis-cli keys "*some-key*" | xargs redis-cli del
```