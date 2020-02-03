# redis-purge
Purge redis keys matching a search value

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
