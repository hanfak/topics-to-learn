# Module 5 Storage and Databases

## Instance Stores and Amazon Elastic Block Store (Amazon EBS)

- Block Level Storage
  - to store files (bytes stored on disk)
  - When data change only change that section
  - Hard drive
  - File systems, databases use it
- Instance STore Volumes
  - storage that can be provided by EC2 instance
  - Physical attached to host that EC2 is running on
  - If EC2 is terminated, the data on the ISV is deleted
    - As the EC2 might start up on another host
  - Useful for temp data, scratch files, data that can be easily recreated without consequence
  - Not good for persisting data outside of lifecycle of EC2
- Amazon Elastic Block Store (EBS)
  - Create virtual Hard drives (volumes) that are attached to the EC2 
  - Not tied to the host
  - persist data outside of lifecycle of EC2
  - Can configure the type you want (size, type) and attach it the EC2
  - Can take incremental back ups of data (snapshots)
    - configurable
    - only the blocks of data that have chagned are saved
  - Up to 16TB
  - SSD by default, but HDD options

## Amazon Simple Storage Service (Amazon S3)

- Data to be stored somewhere
- Store and retrieve unlimited amount of data
- Data stored as objects
  - each object contains data, metadata and key
    - metadate = info about data, how its used, object size
    - key = unique id of object
  - When object is updated, the whole object is modified
  - Stored in buckets
  - Max size of object =5Tb
  - Used for write once read many
  - Each object has a url
  - Can version objects (keep history of object, can rollback if deleted)
  - Create permissions (visibility, write access) for multiple buckets
  - Different tiers/classes
- Storage classes
  - Standard
    - 11 9s of durability (remain intact for one year)
    - for frequent access
    - Multiple copies are stored in 3 availability zones
    - Content distributino
    - data analytics
    - Static web hosting 
      - Load all static files (html etc) to S3 and check box to host it as site
  - Standard Infrequent Access (STandard-IA)
    - For data that is accessed less frequently, but requires rapid access when needed
    - backups, disasted recovery files, or long term storage
    - Audit data, stored for seveal years can be moved to other classes
    - Lower storage price
    - higher retrieval price
    - Multiple copies are stored in 3 availability zones
  - One Zone Infrequent Access
    - 1 copy are stored in 1 availability zones
    - Lower storage price than STandard IA
    - Saving costs on storage
    - Can easily reproduce data incase of failure of zone or loss of data
  - Intelligent Tiering
    - Data with unknown or changing access patterns
    - Monthly monitroing and automation fee per object
    - 
  - Glacier Instant Retrieval
    - For archived data that needs immediate access
    - Access time of milliseconds (same perfromance as standard)
  - Glacier Flexible Retrieval
    - Low cost storage
    - Takes 1 minutes to 12 hours to access data
    - Audit data, stored for several years
    - Use vaults
  - Glacier Deep Archive
    - Lowest cost
    - Retrieve within 12 to 48 hours
    - Long retention
    - aim for 1/2 times a years access
    - Multiple copies are stored in 3 availability zones
  - Outposts
    - Creates buckets on Outposts
    - Easier to retrieve
    - Puts it on your on premise site
- Lifecycle polices
  - Setup rules to move data between tiers
  - ie after x days move to another class
  - Default polics
    - haven’t accessed an object for 30 consecutive days, Amazon S3 automatically moves it to the infrequent access tier, S3 Standard-IA. If you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard.
- EBS vs S3
  - 
## Amazon Elastic File System (EFS)

- A type of file storage
  -  a storage server uses block storage with a local file system to organize files. Clients access data through file paths.
- Ensures that
  - access the same data at the same time
  - Storage can handle the amount of data
  - scale with increase demand
  - that backups are taken
  - data is stored is redundantly
  - management of servers holding data
- EFS handles all this
- EFS
  - Multiple instances can access (read/write) the data in EFS at the same time
  - Linux file system
  - regional resource
  - automatically scales
  - In different availability zones
    - allows for concurrent access
- difference with EBS
  - does not scale, once you attach it to EC2 thats it
  - EBS must be in same availability zone
- Can be AWS cloud service or on prem
  - on prem access with AWS Direct Connect

## Amazon Relational Database Service (RDS)

- RDBS useful for data stored that has relationships with other stored data
- Data is stored in tables
- Tables are defined by schemas
- relationships between data in tables is done via a key
- Querying is done via standard language such as SQL
  - so is defining the schema of the tables (definition)
  - And commands (updates/delets/writes)
- Supported DB
  - postgres
  - mysql
  - oracle
  - sql server
- Security
  - at encryption at rest
  - encryption in tranist
- Migrate database from on prem to aws
  - Lift and shift migration
  - Have more control over  OS, memory, CPU, storage capacity, etc
- Can use Amazon RDBS, a managed db service
  - supportst the major DB engines
  - Hardware provisionin
  - Automated patching
  - backups
  - redundancy
  - failover
  - disaster recovery
- Amazon Aurora
  - enterprise class rdbs
  - a more managed db system
  - mysql or postgres flavours
    - 5 times faster than mysql and 3 time sfaster than postgres
  - Reduces unecessary IO
  - cheaper than other db engines
  - data is replicated across facilities (6 copies at any one time)
  - up to 15 read replicas
  - Continuous back up to S3
- Can be slow, due to the overhead of the queries/commands over several tables
- For business analytics, over many tables

## Amazon DynamoDB

- Serverless DB
- Data stored in tables, as items with attributes
- Handles the storage, automatic scaling, stored redundently accross multiple AZ,
- millisecond respone time
  - Dont have to provision, patch or manage servers, or install, maintain or operate software
- Does not use sql, does not need to define schema
- Useful for data that is not rigid (ie cannot be defined by a scehma) and need high performance
- Non relational db
- Have simple flexible schemas
- Can add/remove attributes to a table at any time
- NOt every item must have the same attributes
- Store data as key-value pairs
  - key = items
  - value = attirbutes
- Queries are much simpler
  - focus on collection of items from one table
  - Not on queries from multiple tables
  - leads to quick response time and high scalability
- It is purpose built and fits a specific usecase
- Most data is used for lookup lists
  - this can be done via non relational DB rather than sqlDB

## Amazon Redshift

- Used for data analysing what happened
- Using traditional RDBMS for querying data which is constantly updated
  - causes performance issues
  - used for high speed real time ingestion, rather than complex queries over ltos of data
  - VAriety of data that is spread out has issues with this analytics
- USe of data wharehousing
  - engineered for big data and historical analystics instead of operational analysis
  - For questions about looking backwards,rather than looking at the current information for current processing (which is what RDBMS is built for)
- Redshift
  - DW that is tuned, resiliant and highly scalable
  - Nodes can handle mutliple PBytes

## AWS Database Migration Service (AWS DMS)

- Help migrate DB onto AWS securly adn easily
- Source DB remains fully operational during the migration
  - reduces the downtime
- Dont have to migrate to the same type of DB
  - Same type migrations = homogenous
    - straigthforward
  - source and target are different = hetrogenous
    - Two step process
      - Need to convert schema structure/data types and db code using AWS Schema Conversion Tool to match the target db
      - Then use DMS to migrate the data
- Can migrate from from on prem to EC2 or RDS
- Other migrations include
  - dev/test db migrations
    - copy prod data to test env (one off or continuously)
  - db consolidations
    - have multipe db but move to one db
  - continous db replication
    - for disaster recovery or geographic separation

## Additional Database SErvices


- Amazon DocumentDB
  - Document db
  - supports MongoDB
- Amazon Neptune
  - graph DB
  - works with highly connected datasets
  - ie recommendation engines, fraud detection, and knowledge graphs.
- Amazon Quantum Ledger Database (Amazon QLDB)
  - review a complete history of all the changes that have been made to your application data.
  - Data never deletd
- Amazon Managed Blockchain
  - create and manage blockchain networks with open-source frameworks.
  - Blockchain is a distributed ledger system that lets multiple parties run transactions and share data without a central authority.
- Amazon ElastiCache
  - adds a caching layer on top of db
  - improve read times for common requests
  - two types: redis and memcached
- Amazon DynamoDB Accelerator
  - in memory cahce for dynamo db
  - millis to micro

## Links

- https://aws.amazon.com/products/storage
- https://aws.amazon.com/blogs/storage/
- https://aws.amazon.com/getting-started/hands-on/?awsf.getting-started-category=category%23storage&awsf.getting-started-content-type=content-type%23hands-on
- https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23storage
- https://aws.amazon.com/dms/
- https://aws.amazon.com/products/databases
- https://aws.amazon.com/getting-started/deep-dive-databases/
- https://aws.amazon.com/blogs/database/
- https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23databases