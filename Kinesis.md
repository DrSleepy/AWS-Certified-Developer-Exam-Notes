# Kinesis

Kinesis handles millions of records being streamed in from a bunch of data sources

- Makes it easy to load and analyse data all that data

**Streams:**

- Data passed into streams are stored for 24 hours (default)
- Data can be stored up to 7 days maximum
- Data is stored on 'shards' inside the stream
- Shards can perform up to 5 transactions per second for reads
- The total capacity of the stream is the sum of all the shards
- The consumers (can be a Lambda, EC2 etc) reading the data in the Shards can save the data wherever they want (DyanmoDB, S3, Redshift etc)

**Firehose:**

- Does not have Shards (taken care for you)
- Firehose is much more automated than Streams
- Firehose does not have a data retention period
- Data passed into Firehose is first analysed (optional) then sent straight into S3, Redshift or ElasticSearch

**Analytics:**

- Allows you to run SQL queries on the data being passed into the Stream or Firehose
- SQL query can save the data to S3, Redshift or ElasticSearch
