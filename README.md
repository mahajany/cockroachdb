### Copied from (..thanks)
https://kb.objectrocket.com/cockroachdb/docker-compose-and-cockroachdb-1151

### Cockroach DB
`docker-compose up`
This shall bring up a DB cluster with two nodes - node_1 and node_2






#### Admin UI
http://localhost:8080/#/overview/list

#### Cockroach DB University
`https://university.cockroachlabs.com/user/consume/course_pathway/7ea6d930-5e1d-3bb8-9647-d0462b2948e1/92/0a11251b-48e0-34cb-ac53-2c6c7c246f3e?complete=0&tab=overview`



#### Access nodes
```
docker exec -it cockroach_node_1 /bin/bash
docker exec -it cockroach_node_1 ./cockroach sql --insecure
 docker exec -it cockroach_node_2 ./cockroach sql --insecure
./cockroach sql --insecure
```

#### Load data
```
docker exec -it cockroach_node_1 /bin/bash
cockroach workload init movr
```
Connect to node-1 --> Load data --> check if movr db / tables etc.are loaded --> exit --> connect to node-2 and Bingo! The movr db should be there.


##### Start a 3 node cluster
```
cockroach start --insecure --join=localhost:26257,localhost:26258,localhost:26259 --listen-addr localhost:26257 --http-addr localhost:8080 --store=cockroach-data-1
cockroach start --insecure --join=localhost:26257,localhost:26258,localhost:26259 --listen-addr localhost:26258 --http-addr localhost:8081 --store=cockroach-data-2
cockroach start --insecure --join=localhost:26257,localhost:26258,localhost:26259 --listen-addr localhost:26259 --http-addr localhost:8082 --store=cockroach-data-3
cockroach init --insecure

```