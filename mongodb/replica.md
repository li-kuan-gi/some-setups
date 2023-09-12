# Create Mongodb Replica set

## Create a Docker Network

``` bash
sudo docker network create mongoCluster
```
This command will create a Docker network.

## Start MongoDB Instances

create 3 instances

```bash
sudo docker run -d --rm -p 27017:27017 --name mongo1 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo1
```
```bash
sudo docker run -d --rm -p 27018:27017 --name mongo2 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo2
```
```bash
sudo docker run -d --rm -p 27019:27017 --name mongo3 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo3
```

## Initiate the Replica Set

```bash
sudo docker exec -it mongo1 mongosh --eval "rs.initiate({
    _id: \"myReplicaSet\",
    members: [
        {_id: 0, host: \"mongo1\"},
        {_id: 1, host: \"mongo2\"},
        {_id: 2, host: \"mongo3\"}
    ]
})"
```

## Show the Connection String

```bash
sudo docker exec -it mongo1 mongosh --eval "rs.status()"
```

## One "click" script

create:

```bash
sudo docker network create mongoCluster && sudo docker run -d --rm -p 27017:27017 --name mongo1 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo1 && sudo docker run -d --rm -p 27018:27017 --name mongo2 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo2 && sudo docker run -d --rm -p 27019:27017 --name mongo3 --network mongoCluster mongo:latest mongod --replSet myReplicaSet --bind_ip localhost,mongo3 && sudo docker exec -it mongo1 mongosh --eval "rs.initiate({_id: \"myReplicaSet\", members: [{_id: 0, host: \"mongo1\"},{_id: 1, host: \"mongo2\"},{_id: 2, host: \"mongo3\"}]})"
```

delete:
```bash
sudo docker stop mongo{1,2,3} && sudo docker network rm mongoCluster 
```