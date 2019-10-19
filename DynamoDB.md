# DynamoDB

- DynamoDB is stored on SSD storage
- By default, it is replicated across 3 geographically distinct data centers
- Choice of 2 consistency models:
  - Eventual consistent reads (default, cheap)
  - Strongly consistent reads (expensive)

## Eventually Consistent Reads

**Eventually consistent reads**
Consistency across all 3 (default) replicas of databases is usually reached within 1 second.
(Best read performance)

**Strongly consistent reads**
A Strongly consistent read returns a result that reflects all writes that recieved a successful
response prior to the read.

## Indecies

Indecies speed up searches as well as giving you extra access patterns (more queries can performed).

**Local Secondary Index (LSI)**

1. Can only be created during creation of the table
2. Cannot add, remove or modify it later
3. Has the same Partition Key as your original table (but a different Sort Key)

**Global Secondary Index (GSI)**

1. Can be created and updated during table creation or after
2. Has different Partition and Sort Keys

## Query and Scan

**Query**

- Searches for a record in the table based on the Partition Key.
- Can filter further with the use of the Sort Key (if present)
- Results are always ordered by the Sort Key
- Order can be reversed using the ScanIndexForward parameter
- by default, Queries are Eventually Consistent
- By default, a Query will return all attributes
- Only selected attributes can be returned with the use of ProjectionExpression (see NOTE: ProjectionExpression below)

**Scan**

- Will scan EVERY item in the table
- By default, a Query will return all attributes+
- Only selected attributes can be returned with the use of ProjectionExpression (see NOTE: ProjectionExpression below)

**_NOTE_: ProjectionExpression**

- ProjectionExpression will read the ENTIRE record (so it will NOT be saving Read Capacity Units)
- ProjectionExpression will however save bandwith as it will now have a SMALLER object to PUSH back to the client
- A solution to this would be to create a GSI with the only NEEDED attributes (this will save RCUs as the entire record will not have to be read BUT you will have to pay for the GSI - your choice)

**Query vs Scan**

- Query is more efficient (cheaper)
- Scan dumps the entire table, then filters out the values to provide the desired result - removing the unwanted data (more steps)
- Scan takes longer the longer the table grows
- On a large table, scan may take up the table provisioned throughput (max RCUs) in a single table

**Improving performance**

- Reduce the impact of a Query/Scan by setting a smaller page size (use pagination, show only 40 results i.e)
- Perform a large number of smaller operations. This will allow other requests to succeed without throttling
- Avoid using Scan
- Configure DynamoDB to use Parallel Scans by logically dividing a table or index into segments and scanning each segment in parallel

## Provisioned Throughput

- Provisioned Throughput is measured in Capacity Units.
- Read Cpacity Units (RCU) and Write Capacity Units (WRU) are specified when creating the table
- RCU and WCU can be updated after table creation
- 1 WRU = 1 x 1KB Write per second
- 1 RCU = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (default)

**Example:**

- A table has 5 RCU and 5 WCU

This configuration will be able to perform:

- 5 x 4KB Strongly Consistent Reads = 20KB per second
- 10 x 4KB Eventually Consistent Reads = 40KB per second
- 5 x 1KB Writes = 5KB per second

If your application reads or writes larger items, it will consume more Capacity Units and will cost you more as well

**Calculation:**
Table and Requirements:
5 RCU
5 WRU
80 records, 3KB each
Strongly Consistent Reads

_What is the total number of RCUs needed to read all 80 records in the table?_

- 1 RCU = 4KB
- 1 record = 3KB
- 3KB / 4KB = 0.75 (RCU)
- Round-up 0.75 to the nearest whole number = 1 (RCU)
- 0.25 RCU (or 1KB) is "wasted" in the RCU
- So this means 1 RCU can handle 1 record
- 80 records. 80 RCUs

Answer: 80 RCUs

For Eventually Consistent Reads, perform the same calculation but divide the end result by 2.
The same calculation is done for Write Capacity Units.

**On-Demand Capacity:**

- Means you do not need to specify your provisioned throughput
- DynamoDb instantly scales up and down the provisioned throughput based on activity of your application
- Great for unpredictable traffic
- You want to pay for only what you use (pay per request)

## Provisioned Throughput Exceeded Exception

ProvisionedThroughputExceededException is an error thrown by the DynamoDB table when your request rate
is too high for your RCU/WRU set on the table.

- AWS SDK will automatically retry the DynamoDB API call until it is successful
- If not using AWS SDK, measures have to be taking in your code to retry the DynamoDB API call
- If not using AWS SDK, try using Exponential Backoff
  - Exponential Backoff is an algorithm that increases the wait time between each retry
  - Exponential Backoff is already implemented by AWS SDK

**Cause for Exception:**

- number of requests is too high

## Transactions

- Supports ACID Transactions (Atomic, Consistent, Isolated, Durable)
  - Atomic: Transation must be treated as a single unit (all or nothing)
  - Consistent: Must leave the database in a valid state. Avoid corruption and data integrity issues
  - Isolated: No dependency between transactions. Can be completed in parallel or not. Should have the same affect
  - Durable: When a transation has been comitted, it must remain committed even have a database failure
- Read or write multiple items across multiple tables as an all or nothing operation
- Check for a pre-requisite condition before writing to a table

## Time To Live (TTL)

- Records with an expired TTL will be marked for deletion WITHIN 48 hours (depends on workload and table size)
- Records will not be deleted as soon as the expiration time is up
- Records with an expired TTL can still be queried and updated
- The TTL can still be updated even after it is "expired"

## Streams

- Triggered when theres an INSERT, UPDATE OR DELETE action on the table
- Trigger in order
- Logs are encrypted at rest
- Logs are stored for 24 hours
- Accessed using a dedicated endpoint (ARN)
- By default, the Partition Key is Recorded
- Before and After images can be captured
- Events are recorded in near real-time
- Can be linked to a lambda
