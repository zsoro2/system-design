# Transactions

A transaction groups several reads and writes into a single unit. It either completes successfully (commit) or fails (rollback).

## ACID Properties of a Transaction

The safety guarantees provided by transactions are often described by the well-known acronym ACID.

- **Atomicity**: Ensures that all operations within a transaction are completed; if not, the transaction is aborted and any changes are undone.
- **Consistency**: Ensures that a transaction takes the database from one valid state to another, maintaining data integrity.
- **Isolation**: Ensures that transactions do not interfere with each other, preventing concurrency issues.
- **Durability**: Guarantees that once a transaction is committed, it remains so, even in case of a system failure, even if there is a hardware fault or the database crashes. Involves a write-ahead log.

## Transaction Isolation Levels (MySQL + PostgreSQL)

1. **READ UNCOMMITTED (weakest)**
    - **Explain**: With this isolation level, transactions can read UNCOMMITTED data from other transactions, leading to dirty reads.
    - **Example**:
        1. T1 and T2 start.
        2. T1 updates a specific record with a new value.
        3. T2 selects this record and gets the new value (this is a dirty read because T1 transaction is not committed yet, but T2 sees the new value).
    
2. **READ COMMITTED**
    - **Explain**: The transaction can only read the COMMITTED data, preventing dirty reads.
    - **Example**:
        1. T1 and T2 start.
        2. T1 updates a specific record with a new value.
        3. If T2 selects the same record, it will get the original data, not what T1 updated.
    
3. **REPEATABLE READ (default level)**
    - **Explain**: Transactions see consistent data during their execution, blocking non-repeatable reads but not phantom reads.
    
4. **SERIALIZABLE (strongest)**
    - **Explain**: This level locks the rows, preventing other transactions from modifying them until the transaction is committed.
    - **Example**: T1 will timeout or succeed as soon as T2 is committed.

## Concurrency Issues (Race Conditions)

Come into play when one transaction reads data that is concurrently modified by another transaction, or when two transactions try to simultaneously modify the same data.

- **Dirty Reads**: A transaction reads uncommitted data from another transaction.Imagine a transaction has written some data to the database, but the transaction has not yet committed or aborted. Can another transaction see that uncommitted data? If yes, that is called a dirty read. One client reads another client’s writes before they have been committed.
- **Dirty Writes**: What happens if the earlier write is part of a transaction that has not yet committed, so the later write OVERWRITES an uncommitted value? This is called a dirty write.
- **Read Skew (Non-repeatable Reads)**: A transaction reads committed data multiple times but sees different values because another transaction has committed changes in between. 
- **Lost Updates**: Two clients concurrently perform a read-modify-write cycle. One overwrites the other’s write without incorporating its changes, so data is lost.
- **Write Skew**: A transaction reads a value, makes a decision based on that value, but the premise of the decision is no longer true by the time the write is made.
- **Phantom Reads**: A transaction reads a set of rows that satisfy a condition, and another transaction inserts, updates, or deletes rows that would affect the initial transaction’s result set if the same query were re-executed.
- **Two-phase locking**: Writers don’t just block other writers; they also block readers and vice versa.



## Solutions for Common Problems

1. **Avoid Read-Modify-Write Cycle**
    - Focus on 'balance = balance - 100' section. Instead we select and then update, based on the selection value, we update with a variable.
    ```sql
    UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;
    ```
2. **Row Level Locking**
    - Focus on 'for update' section.
    ```sql
    SELECT balance FROM accounts WHERE user_id = 1 FOR UPDATE;
    ```
3. **Turn on SERIALIZABLE Isolation Level**
    - Note: This can cause some performance issues.
    ```sql
    set transaction isolation level read uncommitted;
    ```

4. **Optimistic Locking**
    - Allows multiple transactions to complete without locking the database.
    - Steps:
        1. Add a version column:
            ```sql
            ALTER TABLE your_table ADD COLUMN version INT DEFAULT 0;
            ```
        2. Select based on the version column and other conditions:
            ```sql
            SELECT id, name, version FROM your_table WHERE id = 1;
            ```
        3. Update the row based on the version:
            ```sql
            UPDATE your_table
            SET name = 'new_name', version = version + 1
            WHERE id = 1 AND version = 0;
            ```


 
## Resources:

[!ref target="blank" text="Production use"](https://www.youtube.com/watch?v=wEsPL50Uiyo
)
[!ref target="blank" text="Solutions"](https://www.2ndquadrant.com/en/blog/postgresql-anti-patterns-read-modify-write-cycles/)

