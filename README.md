# sharding_workshop

**Step : 1 Create 2 shard M30 Cluster on MongoDB Atlas **
 - Make sure mongo shell is installed on the loacal m/c
 - try to connect to MongoDB cluster from local m/c
      mongosh "mongodb+srv://shardtest.pyuze.mongodb.net/myFirstDatabase" --username <username>
      Password : 
 
**Step 2 : Verify sharding status **
 
 connect to mongodb shell and run below commands :
  -  sh.status()
  -  db.adminCommand( { listDatabases : 1 } )
 
 Step 3 : Load sample dataset from Atlas and repeat step 2
 
 - Discussion on observations
 - is cluster balanced ? How did we idenfy it ? what can be done incase not balanced ?
 
 Step 4 :  make cluster balanced using movePrimary command
 
 - db.adminCommand( { movePrimary: <databaseName>, to: <newPrimaryShard> } )
  - db.adminCommand( { movePrimary : "test", to : "shard0001" } ) (example)
 
 This is OK for current data balancing but how do we make sure this does not happen in future 
 
 - sh.enableSharding( <database>, <primary shard> )
   - sh.enableSharding( test, shard0001 ) - While creating the database
 
 Note : All unsharded collections will go to primary shard only
 
 Step 5 : Now we will showcase how MongoDB can distribute the data automatically by sharding collections
 
 - Create sharded database 
 
