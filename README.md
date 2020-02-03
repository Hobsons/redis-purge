# redis-purge
Purge redis keys matching a search value. Must be run from a system or proxy with access to elasticache for the script to connect to redis

```
$ go run scrubRedis.go
Usage:

[REDIS_ADDR=...]           \
[DELETE_MATCHING_KEYS=yes] \
[REQUIRED_MATCH_COUNT=n]   \
[SIZE_THRESHOLD=x]         \
	/var/folders/m4/_bpm7k_57qj05m8lq4wcgj7w0000gp/T/go-build500872978/b001/exe/scrubRedis [value]

Deletes all keys with a given value if run with DELETE_MATCHING_KEYS=yes
or DELETE_MATCHING_KEYS=y in the environment, otherwise lists the keys with
the given value.

If SIZE_THRESHOLD is set to a number of bytes in the environment, only keys
with values at least as large as SIZE_THRESHOLD will be considered.

If REQUIRED_MATCH_COUNT is a number >0, then keys are selected if the value
contains the search pattern _at least_ that many times.
exit status 1
```


example:


```
$ go build ./redis-purge.go

$ DELETE_MATCHING_KEYS=y REDIS_ADDR=session-cache.ore.starfishsolutions.com:6379 REQUIRED_MATCH_COUNT=3 SIZE_THRESHOLD=10000 ./redis-purge '<saml2p:AuthnRequest'
> deleting keys with value matching Search="<saml2p:AuthnRequest" (size>=10000 bytes) (match >= 3 occurrences)
DELETE 1021E27775BB6807EB110AEB752A18B7
DELETE B84D1907C8C6BBB3615EE57FF7F8A6D8
DELETE 0D1F39461DB508DD48E7CA3A51523B28
...
> deleted 75 keys (147289133 total size) matching Search="<saml2p:AuthnRequest" (size>=10000 bytes) (match >= 3 occurrences), 0 keys failed delete
```


#Install

```
go get github.com/go-redis/redis
go build redis-purge
```
