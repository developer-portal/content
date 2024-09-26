## Running a Cassandra cluster

One of the main features of Apache Cassandra is its ability to run in a multi-node setup, providing the
following benefits:

- Fault tolerance: Data is automatically replicated to multiple nodes for fault-tolerance. Replication
  across multiple data centers is supported. Failed nodes can be replaced with no downtime.

- Decentralization: There are no single points of failure. There are no network bottlenecks. Every node
  in the cluster is identical.

- Scalability & Elasticity: Capability to run with dozens of thousands of nodes with petabytes of data.
  Read and write throughput both increase linearly as new machines are added, with no downtime or interruption
  to applications.

### Clearing existing data

If the server was started before or it's already running, all the existing data must be deleted,
the reason for this is because all nodes must have the same `cluster_name` and it's better to
choose a different one from the default `Test cluster` name.

The following commands must be executed on each node:

```
$ sudo systemctl stop cassandra
$ sudo rm -rf /var/lib/cassandra/data/system/*
```

### Configuring the cluster

The Cassandra main configuration file `/etc/cassandra/cassandra.yaml` needs to be edited to setup the
cluster. The parameters that need to be modified are:

- `cluster_name`: Name of your cluster.

- `num_tokens`: Number of virtual nodes within a Cassandra instance. This is used to partition the data
  and spread the data throughout the cluster. The recommended value is 256.

- `seeds`: Comma-delimited list of the IP address of each node in the cluster.

- `listen_address`: The IP address or hostname that Cassandra binds to for connecting to other Cassandra
  nodes. It defaults to localhost and needs to be changed to the IP address of the node.

- `rpc_address`: The listen address for client connections (CQL protocol).

- `endpoint_snitch`: Set to a class that implements the IEndpointSnitch. Cassandra uses snitches for
  locating nodes and routing requests. The default one is `SimpleSnitch` but we will change to
  `GossipingPropertyFileSnitch` which is more suitable for production environments:

  - `SimpleSnitch`: Used for single-datacenter deployments or single-zone in public clouds. Does not
    recognize datacenter or rack information. It treats strategy order as proximity, which can improve cache
    locality when disabling read repair.

  - `GossipingPropertyFileSnitch`: Recommended for production. The rack and datacenter for the local
    node are defined in the cassandra-rackdc.properties file and propagated to other nodes via gossip.

- `auto_bootstrap`: This parameter is not present in the configuration file, so it has to be added and
  set to false. It makes new (non-seed) nodes automatically migrate the right data to themselves.

Configuration files for a 2-node cluster:

Node 1:

```
cluster_name: 'My Cluster'
num_tokens: 256
seed_provider:
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
        - seeds: 10.0.0.1, 10.0.0.2
listen_address: 10.0.0.1
rpc_address: 10.0.0.1
endpoint_snitch: GossipingPropertyFileSnitch
auto_bootstrap: false
```

Node 2:

```
cluster_name: 'My Cluster'
num_tokens: 256
seed_provider:
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
        - seeds: 10.0.0.1, 10.0.0.2
listen_address: 10.0.0.2
rpc_address: 10.0.0.2
endpoint_snitch: GossipingPropertyFileSnitch
auto_bootstrap: false
```

### Starting the cluster

The final step is to start each instance of the cluster, the seed instances must be started first,
then the remaing nodes.

```
$ sudo systemctl start cassandra
```

### Checking the cluster status

The cluster status can be checked with nodetool utility:

```bash
$ sudo nodetool status

Datacenter: datacenter1
===============
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address      Load       Tokens       Owns    Host ID                               Rack
UN  10.0.0.2  147.48 KB  256          ?       f50799ee-8589-4eb8-a0c8-241cd254e424  rack1
UN  10.0.0.1  139.04 KB  256          ?       54b16af1-ad0a-4288-b34e-cacab39caeec  rack1

Note: Non-system keyspaces don't have the same replication settings, effective ownership information is meaningless
```
