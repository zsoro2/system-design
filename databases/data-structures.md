# Data structures

Data Structure  | Best for	 {.compact} | Key Points
---    | --- | ---
Hashmaps | Fast lookups | In memory, loses data if off, no range queries
B-Trees | Database searches	 | On disk, supports range queries
LSM Trees | Heavy writing | Writes to memory first, then sorted to disk

-------

## Hasmaps
- **Best for**: Fast lookups in memory.
- **Key Points**:
    - Data is kept in memory.
    - Loses data if the computer shuts down.
    - Slow on disk.
    - No range queries.

## B-Trees
- **Best for**: Databases with lots of searches.
- **Key Points**:
    - Data is always on disk.
    - Good for range queries.
    - Efficient for frequent searches, inserts, and deletes.
    - Used in file systems and database indexes (e.g., MySQL, PostgreSQL)

## LSM Tree (mostly nosql like Cassandra)
- **Best for**:  Heavy writing.
- **Key Points**:
    - Writes data to memory first.
    - Moves data to disk in sorted order when memory is full, called SSTable.
    - Reading can get slower with more and more SSTable created on disk.
    - Widely used in NoSQL databases like Cassandra, HBase, and LevelDB.
    - Supports high scalability and can handle large datasets efficiently.

-------
## In Summary
- Hashmaps: Fast lookups in memory, used for caching or in-memory databases.
- B-Trees: Efficient on-disk storage, used in relational databases for indexing.
- LSM Trees: High write throughput, used in NoSQL databases for handling heavy writes.
