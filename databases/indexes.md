# Indexes


Index Type | Best For | Key Points | Strengths | Limitations
--- | --- | --- | --- | ---
B-Tree | General-purpose indexing | Balanced tree, keeps data sorted | Efficient searches, range queries | Needs space and maintenance as it grows
Hash | Exact match lookups | Hash table, maps keys to values | Extremely fast exact match lookups | No range queries, needs collision handling
Full-Text | Text search | Inverted index, tracks word occurrences | Handles complex text searches | Resource-intensive, needs extra storage
Clustered | Organizing rows by index key | Stores actual table data at index leaf level | Fast for retrieving ordered rows | Slower for inserts/updates due to reordering
Non-Clustered | Quick access to data | Separate from table, contains pointers to data | Efficient for quick lookups | Can be slower for large datasets compared to clustered
Spatial | Geospatial queries | R-Trees, Quadtrees for spatial data | Efficient for location-based queries | Complex to implement, can degrade with irregular data


## B-Tree Indexes
General-purpose indexing in databases.
- **Key Points:**
  - **Structure:** Balanced tree; keeps data sorted.
  - **Performance:** Good for finding specific values and range queries.
  - **Uses:** Common in MySQL, PostgreSQL, Oracle.
- **Strengths:**
  - Efficient searches, inserts, and deletes.
  - Supports range queries.
- **Limitations:** Requires more space and maintenance as it grows.

## Hash Indexes
Fast lookups for exact matches.
- **Key Points:**
  - **Structure:** Hash table; maps keys to values.
  - **Performance:** Very fast for finding exact matches.
  - **Uses:** In-memory databases like Redis; some uses in MySQL.
- **Strengths:**
  - Extremely fast exact match lookups.
- **Limitations:**
  - No range queries.
  - Needs handling for hash collisions.

## Full-Text Indexes
Searching large text fields.
- **Key Points:**
  - **Structure:** Inverted index; tracks occurrences of each word.
  - **Performance:** Optimized for text search.
  - **Uses:** Elasticsearch, MySQL, PostgreSQL for full-text search.
- **Strengths:**
  - Handles complex searches (e.g., relevance, ranking).
- **Limitations:**
  - Can be resource-intensive.
  - Requires additional storage space.

## Clustered Indexes
With a clustered index the rows are stored physically on the disk in the same order as the index. Therefore, there can be only one clustered index.
- **Key Points:**
  - **Structure:** Stores actual table data at the leaf level of the index.
  - **Performance:** Fast for retrieving rows in sorted order.
  - **Uses:** Each table can have only one clustered index (e.g., primary key in SQL Server).
- **Strengths:**
  - Fast data retrieval for ordered data.
- **Limitations:**
  - Slower for insert and update operations due to reordering.

## Non-Clustered Indexes
With a non clustered index there is a second list that has pointers to the physical rows. You can have many non clustered indices, although each new index will increase the time it takes to write new records.
- **Key Points:**
  - **Structure:** Separate from the table; contains pointers to the data.
  - **Performance:** Good for queries that don't require sorted data.
  - **Uses:** Multiple non-clustered indexes can exist per table.
- **Strengths:**
  - Efficient for quick lookups.
- **Limitations:**
  - Can be slower than clustered indexes for large datasets.


## Spatial Indexes
Geospatial queries and multi-dimensional data.
- **Key Points:**
  - **Structure:** R-Trees, Quadtrees, etc.; organizes spatial data.
  - **Performance:** Efficient for spatial operations.
  - **Uses:** GIS, spatial databases like PostGIS, MySQL.
- **Strengths:**
  - Efficient for location-based queries.
- **Limitations:**
  - Complex to implement.
  - Performance can degrade with irregular data.