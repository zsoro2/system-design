# Replication

## Overview
Replication in databases is a technique used to ensure data redundancy and high availability by copying and maintaining database objects in multiple databases that make up a distributed database system. There are several types of replication strategies, each with its own use cases, advantages, and challenges.

## Types of Replication

### Single-Leader Replication

#### Leader
- **Role**: The primary node handling all write requests.
- **Responsibilities**: Accepts write requests, updates local data, propagates changes to followers.

#### Follower
- **Role**: Secondary nodes that replicate the leader's data.
- **Responsibilities**: Receive and apply data changes from the leader, serve read requests.

#### Read-Write Dynamics
- **Writes**: Only accepted by the leader.
- **Reads**: Distributed across followers to balance load and improve read performance.

#### Advantages
- Simplifies conflict resolution since only one node handles writes.
- Ensures data consistency at the leader.

#### Disadvantages
- Can be slow, if done synchronously.
- Single point of failure unless proper failover mechanisms are in place.

### Multi-Leader Replication

#### Use Cases
- Suitable for high availability and geographically distributed systems.
- Allows multiple nodes to accept write requests.

#### Write Conflicts
- **Conflict Detection**: Conflicts are detected asynchronously.
- **Resolution Strategies**: Application-specific logic, Last Write Wins (LWW), vector clocks, and CRDTs.

#### Advantages
- Provides higher write availability and fault tolerance.
- Reduces latency for geographically distributed nodes.

#### Disadvantages
- Increased complexity in conflict detection and resolution.
- Potential for data inconsistency if conflicts are not properly resolved. You can decide to implement some algorithm to automatically resolve conflicts in a consistent manner (e.g., using a unique ID composed of timestamp and randomly generated).


| Feature                      | Single-Leader Replication                           | Multi-Leader Replication                          |
|------------------------------|----------------------------------------------------|--------------------------------------------------|
| **Write Handling**           | Only one leader handles all write operations       | Multiple leaders can handle write operations     |
| **Read Handling**            | Reads are spread across followers                  | Reads and writes can be handled by any leader    |
| **Conflict Resolution**      | Easier, as only the leader handles writes          | More complex, requires resolving conflicts between leaders |
| **Write Availability**       | Limited to the leader's capacity                   | High, as writes can go to multiple leaders       |
| **Fault Tolerance**          | Leader is a single point of failure                | Higher, with multiple leaders providing redundancy |
| **Latency**                  | Higher for nodes far from the leader               | Lower for geographically distributed nodes       |
| **Complexity**               | Simpler to implement and manage                    | More complex due to conflict resolution needs    |
| **Consistency**              | Stronger, easier to ensure immediate consistency   | Eventual consistency, harder to guarantee immediate consistency |
| **Best Use Cases**           | Good for read-heavy workloads                      | Good for high availability and geographically distributed systems |
| **Replication Lag**          | Typically lower due to single write path           | Can be higher due to asynchronous conflict resolution |
| **Failure Recovery**         | Promote a follower to be the new leader            | Complex, involves resolving conflicts between leaders |
| **Examples**                 | Common in databases like MySQL, PostgreSQL         | Used in systems like Apache Cassandra, CouchDB   |
| **Operational Overhead**     | Lower, due to single-leader management             | Higher, due to managing multiple leaders and conflicts |



## Replication Techniques

### Synchronous Replication
- **Mechanism**: Ensures data is written to the leader and at least one follower before acknowledging the write.
- **Pros**: Reduces inconsistency.
- **Cons**: Can impact performance and availability if synchronous followers experience downtime.

### Asynchronous Replication
- **Mechanism**: Data is written to the leader first and then asynchronously propagated to followers.
- **Pros**: Improves write performance.
- **Cons**: Increases the window for potential inconsistency.

## Setting Up New Followers

### Process
1. **Snapshot**: Take a consistent snapshot of the leader’s database.
2. **Copy Snapshot**: Transfer the snapshot to the new follower.
3. **Catch-Up**: The follower requests and applies changes from the leader that occurred since the snapshot.
4. **Synchronization**: Once caught up, the follower processes ongoing changes in real-time.

## Replication Logs

### Write-ahead Log (WAL) Shipping
- **Description**: Logs every modification and ships these logs to followers.
- **Pros**: Simple, works at a low level.
- **Cons**: Coupled to storage engine, may require downtime for upgrades.

### Logical (Row-based) Log Replication
- **Description**: Uses a log format decoupled from the storage engine, recording changes at the row level.
- **Pros**: Easier upgrades and external parsing.
- **Cons**: More complex to implement than WAL shipping.