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
              shard1a    port 27030;
              shard1b    port 27031; 
              shard1c    port 27032
              
Shard-2 server:-
              shard2a   port 27040;
              shard2b   port 27041;
              shard2c   port 27042
             
