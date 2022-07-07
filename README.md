# Snowflake-Cheatseat
Snowflake's most frequently needed commands gathered in one place

### What's my current user, role, warehouse, database, etc?
```
SELECT CURRENT_USER();
SELECT CURRENT_ROLE();
SELECT CURRENT_WAREHOUSE();
SELECT CURRENT_DATABASE();
```
### How do I create a new database user?
```
SHOW ROLES;
USE ROLE ACCOUNTADMIN;
-- USE ROLE SECURITYADMIN;
CREATE USER {username} PASSWORD = '{password}' MUST_CHANGE_PASSWORD = TRUE;
-- Grant usage on a database and warehouse to a role
SHOW GRANTS TO ROLE {role};
GRANT USAGE ON WAREHOUSE {warehouse} TO ROLE {role};
GRANT USAGE ON DATABASE {database} TO ROLE {role};
```








Snowflake Concepts and Terminology Cheat Sheet
clone = a clone is a copy of a storage object (database / schema / table). This is typically a zero-copy clone, meaning the underlying data exists only once but metadata creates 2 different entities on top of the base data.

credits = compute credits are the unit of compute in Snowflake. One credit is charged for one node running for one hour in Snowflake. Larger warehouses consist of more nodes and therefore charge more credits per hour.

data sharing = secure data sharing is a unique feature of Snowflake that allows account-to-account sharing of data. This allows producers to securely expose storage objects (databases / schemas / tables) to consumers. The sharing is live and has a wide range of configurations to ensure the desired billing of storage and compute.

database = a database is the top-level storage object in Snowflake. All storage objects are contained within a database. This is the highest level of data organization available.

file format = a named file format is a collection of rules for processing file data to and from Snowflake stages. File format rules include data formatting, extension-specific options (like skipping headers in CSV files), and error tolerance options (like skipping files with too many errors).

materialized view = a materialized view is a stored query against 1 underlying table (this restriction may change in the future) that automatically runs behind the scenes. The query results are stored (materialized), which can improve read latency.

privilege = privileges are definitions of specific access permissions to specific objects. In Snowflake’s security model, privileges on objects are granted to roles. Roles are granted either to users or other roles. Privileges are never directly assigned to users.

role = a role is the unit of Snowflake security to which privileges can be granted to or revoked from. Roles are not users but are assigned to users to authorize user activity.

schema = a schema is the second layer of storage organization in Snowflake below a database. They are containers that hold tables, views, stages, and other bottom-level objects. Security objects and warehouses are not stored at this level. A schema and a database together define a namespace in Snowflake.

sequence = a sequence is a generator object that creates unique values in SQL statements that cover many rows. This is an advanced SQL concept. Check out this article that gives an overview of the concept.

Snowpipe = this refers to Snowflake’s continuous loading solution. It is confusing right now because Snowpipe is being upgraded for asynchronous file handling through queues, but not all instances will have this ability (auto ingest). In short, all Snowpipes make regular file ingestion from external stages more manageable for your production workflows.

SnowSQL = SnowSQL refers to the Snowflake CLI tool. It’s also commonly used to refer to the actual SQL code that is run in Snowflake.

stage = this is a file location used for data ingestion. Stages can either be internal (managed by Snowflake) or external (managed by you). Stages are just S3 (AWS) or Blob Storage Containers (Azure) where data in Snowflake-supported file formats can be stored before loading into a Snowflake table. Understanding stages is critical to building production data pipelines.

stored procedures = stored procedures are reusable functions defined with a mix of JavaScript and SQL for advanced functionality. These are useful for implementing logic with advanced control flow requirements that are unsupported by SQL (error handling, for-loops, conditional branching).

streams = streams are change records on top of tables. They are queryable like normal tables but include an automatically-updated record of every data change that occurred on the target object. These are a preview feature, so make sure you have it enabled.

table = a table is the lowest level object in Snowflake. It is a structured collection of persisted data.

tasks = a task is a SQL statement executed either on a schedule or in response to the completion of another task. Tasks are useful for job scheduling and are currently preview features.

temporary table = these tables exist only for the duration of a session and are not queriable by any other user. This is useful for ETL processing and helps reduce storage costs as temp tables do not use the same amount of failsafe storage that a standard table does.

time travel = this feature enables users to query data at different points within a range of time (configured at the storage object level). The longer the range of time (up to 90 days, but 1 day by default), the more storage charges are incurred. This feature is valuable for comparing state over time without having to manage additional complex storage structures.

transaction = a transaction is a collection of SQL statements that must either be entirely executed successfully or entirely unexecuted (no partial execution). These transactions are fully ACID compliant.

transient table = transient tables are really similar to temporary tables, but they persist beyond a single session and can be queried by other users. They differ from standard tables by having no failsafe storage, making them cheaper but less durable.

UDF (user-defined function) = a UDF is a named collection of either SQL or JavaScript logic that accepts arguments and returns either a scalar (single value) or series of rows, depending on how it is defined. It does not support the creation or modification of objects (DML) and only returns newly computed values.

user = a user is an entity of authentication. Authorization is granted to users through roles. Roles are a named collection of 0 or more privileges to perform actions with Snowflake objects. Users are often associated with individuals but are also used to authenticate services, such as BI connections.

view = a view is a table-like object that can be queried but stores no actual data. The structure of a view is defined when it is created as a SQL statement that selects from other underlying objects (including other views).

warehouse = a virtual warehouse is the object of compute in Snowflake. The size of a warehouse indicates how many nodes are in the compute cluster used to run queries. Warehouses are needed to load data from cloud storage and perform computations. They retain source data in a node-level cache as long as they are not suspended. Snowflake credits are billed for a 1-node (XSMALL) warehouse running for 1 hour (10-second minimum charge, prorated per second of run after that).

`**worksheet**` = a worksheet is a tab within the Snowflake Web UI with its own distinct context from the user’s logged-in context. Each worksheet has a SQL editor space where SQL is commonly developed and ran in one location.
