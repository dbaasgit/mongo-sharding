# mongo-sharding
Deploying and configuring the mongo shard on linux machine.
Here I'm going to deploy mongosharding with two sharded cluster and each shard have 3(P-S-S) nodes and 3(P-S-S) configuration cluster and one Mongos.
As I have only one machine so I'm deploying all the above node on a single machine, so we have total 10 running mongo instances on single machine.


Architecture:-

config server:- 
              mongodconf1 port 27050;
              mongodconf2 port 27051;
              mongodconf3 port 27052
              
Shard-1 servers:-
              mongo_shard1a    port 27030;
              mongo_shard1b    port 27031; 
              mongo_shard1c    port 27032
              
Shard-2 server:-
              mongo_shard2a   port 27040;
              mongo_shard2b   port 27041;
              mongo_shard2c   port 27042
             
mongos port 27017

Steps:-

1st:- install monngod successfully on the server(my version was 4.4).

2nd:- create the data and log directory for each node (for config, shard1 and shard2 and mongos) 

3rd:- change the group permission to those directories sudo chown -R mongod:mongod <directory>

4th:- create configuration file for each node in /etc dir.

  (mongod_shard1a.conf
mongod_shard1b.conf
mongod_shard1c.conf
mongodconf1.conf
mongodconf2.conf
mongodconf3.conf
mongos.conf
mongod_shard2a.conf
mongod_shard2b.conf
mongod_shard2c.conf
)

5th:- creating services in /usr/lib/systemd/system/   dir [use touch command ex. sudo touch mongod_shard1a.service]
  
  (mongod_shard1a.service
mongod_shard1b.service
mongod_shard1c.service
mongod_confserv1.service
mongod_confserv2.service
mongod_confserv3.service
mongos.service
mongod_shard2a.service
mongod_shard2b.service
mongod_shard2c.service)
  
 6th:- now create mongod binary in /usr/bin/  dir [use cp command ex. sudo cp mongod mongod_shard1a. and dont create for mongos or mongod as it already been created by Default when we install mongo]
  
  ( mongodconf1
 mongod_shard1a
 mongod_shard1b
 mongod_shard1c
 mongodconf2
 mongodconf3
 mongod_shard2a
 mongod_shard2b
 mongod_shard2c
)
  
  
7th:- now its time to enable the services one by one that we created above, the command is sudo systemctl enable mongod_confserv1.service
  
8th :- once all the services are up its time to start each mongo nodes  one by one, the command is sudo systemctl start mongod_confserv1.service
  
9(a)connect to the one of the config node and enable the replication for the congifg cluster
 
 (b)connect to shard1 node and enable the replication for the shard1 cluster
 
 (c)connect to shard2 node and enable the replication for the shard2 cluster
 
 (d)connect to mongos node and both the shard in mongos
  
      
