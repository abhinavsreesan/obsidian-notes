[[Kafka]]

REF: [Introducing KSQLDB!!! Database on streams](https://medium.com/datapebbles/introducing-ksqldb-database-on-streams-1b6f28f2882c)
- Specialized Java based DB optimized for stream processing
- Runs on its own cluster adjacent to the Kafka cluster
- It allows for stream processing jobs written in SQL
- It has a docker image and has a rest api
- Has Kafka connect integration to query external data sources

**Streams and Tables**: A stream is an immutable, append-only sequence of events that represents the history of changes. The table contains the current status of the events, which is the result of many changes. ksqlDB creates the relations with Kafka topic data by creating schema on the top of it.

**Materialized view**: Converting the stream of events into a table with all the required changes is called materializing. A materialized view is also known as stateful aggregation.

**Push Queries**: A push query is a form of query issued by a client that subscribes to a result as it changes in real-time. It’s a continuous query that pushes the incremental result to the client in real-time. Push queries enable you to query a stream or materialized table with a subscription to the results

**Pull Queries**: A pull query is a form of query issued by a client that retrieves a result as of “now”, like a query against a traditional RDBMS. Pull queries enable you to fetch the current state of a materialized view. Because materialized views are incrementally updated as new events arrive.

**Connect**: Kafka connect is an open-source component of Apache Kafka. It loads and exporting of data from an external system to Kafka. Ksql provides the functionality to create, describe, and import topics from connect to ksqlDB.