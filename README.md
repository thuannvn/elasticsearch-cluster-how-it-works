# Elasticsearch Cluster - How It Works
https://blog.techblogsearch.com/2018/11/29/elasticsearch-cluster-understanding-how-it-works/

![](https://www.elastic.co/assets/blt47da469cfb3097c3/cluster-topology.svg)

## Questions will be solved
- [x] How a node in cluster talks to others?
- [x] What happens when a node joins or leaves the cluster?
- [x] What happens when a node stops or has encountered a problem?
- [x] What is the role of master/client/data in cluster ?
- [ ] What is memory requirement for each node ?
- [ ] How ES organizes data ?

## What is a cluster of nodes ? 
- Start a ES instance => a cluster of single node.
- Start another ES instance with the same `cluster.name` => a cluster of 2 nodes.
- How nodes talk to each other: `Over TCP`
- How nodes talk to external: `JSON over HTTP`
- Each node can play one or more roles in cluster.

## What is role of master/client/data ?
### Master
- Create/Delete `indices`
- Add/Remove `nodes` from cluster
- Broadcast changes to other nodes
- Only 1 master node at a time.

### Data
- Holding `data` in the shards => CRUD, search, aggregations on `data`

### Client
- Routing requests to master/data => `smart router`

## Adding a node to cluster
- It will ping all nodes => find master node => request to join => accepted & joined.
- If joined node is data => the master will re-allocate data to this node.

## Removing a node to cluster
- The master node will remove this node from cluster, broadcast changes the all nodes.
- If removed node is data => the master will re-allocate data.
- If remove node is master => one of the other master nodes will be elected to be master ( Fault Detection )

## How ElasticSearch organizes data ?
- Elasticsearch as MySQL
  * Index <=> Database
  * Type <=> Table
  * Document <=> Row
  * Field <=> Column
- Index is one or more `shards` distributed on muliple nodes
- Number of primary shards can NOT be changed after index created

# References:
- https://medium.com/@duy.do/how-elasticsearch-cluster-works-97d537071b87
- http://solutionhacker.com/elasticsearch-architecture-overview/
- https://www.slideshare.net/PetarDjekic/elasticsearch-101-cluster-setup-and-tuning
