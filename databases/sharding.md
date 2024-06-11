# Sharding and Partitioning

## Introduction
Sharding and partitioning are techniques used to distribute data across multiple machines to improve performance and scalability. The goal is to spread the data and query load evenly, avoiding hot spots and ensuring efficient data management.

## Key Concepts

### Skewed Partitioning
**Definition:** When the partitioning is unfair, causing some partitions to have more data or queries than others. This imbalance can degrade performance and lead to hot spots.

### Hot Spot
**Definition:** A partition with a disproportionately high load. This can lead to performance bottlenecks and inefficient resource utilization.

### Rebalancing
**Definition:** The process of moving load from one node in the cluster to another to ensure even distribution of data and queries. This is crucial when nodes are added or removed from the cluster.

### Hash Partitioning
**Definition:** A method that uses a hash function to determine the partition for a given key. This helps in distributing the data evenly across partitions.

### Consistent Hashing
**Definition:** A specific type of hash partitioning that aims to minimize the amount of data that needs to be moved when nodes are added or removed. It helps in maintaining a balanced load.

Each object key will belong in the server whose key is closest, in a counterclockwise direction

[![Image from www.toptal.com](/images/consistent_hashing.png)](www.toptal.com)



