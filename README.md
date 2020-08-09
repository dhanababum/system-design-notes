# system-design-notes

## Redis
#### Key-Value Store
* Redis is Key-Value store NoSql database
* Key is a string, value is pretty much anything
* Redis is in memory fast
* Set key with expiry
* Single Threaded(Except when durability is enabled)
#### Optional Durability
* Journaling(append only log AOP)(What happend to the system{someone inserted key, some one deleted key, etc.. can trace})
* Snapshotting
* Both happen asynchronously in the background
#### Transport Protocal
* Uses TCP
* Reuqest/Response just like HTTP
* Message format is RESP(REdis Serialization Protocol)
#### Pub/Sub
* Redis Supports Publish Subscribe model
* Push model support
#### Replication/Clustering(Avalability)
* Replication - One Leader many followers model
* Clustering - Shard data accross multiple nodes
* Hybrid(both Replication/Clustering)
#### Operations
* Set key value
* Set key with Expiry
* get Key
* Exists key
* del key
#### Setup
* Docker spinup
* default port 6379

## ZeroMQ
#### What is ZeroMQ?
* Messaging Library(20 languages)
* 5 messaging Patterns
* Brokerless
* You build what you need
* Not Sure why it's called MQ
#### Messaiging Patterns
* Sychronous Request/Response
* Asynchronous Request/Response
* Publish/Subscribe
* Push/Pull
* Exclusive Pair
#### Socket Types
* REQ(Request)
* REP(Reply)
* PUSH
* PULL
* DEALER(Client)
* ROUTER(Server)
