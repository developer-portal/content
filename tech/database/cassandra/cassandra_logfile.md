## Log file

The package logs to `/var/log/cassandra/system.log` by default.

## nodetool utility

The nodetool utility is a command-line interface for monitoring Cassandra and performing routine
database operations.

```bash
$ sudo nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address    Load       Tokens       Owns (effective)  Host ID                               Rack
UN  127.0.0.1  143.43 KiB  256          100.0%            94becf56-8a2a-4935-bdf0-79e24694d207  rack1
```
