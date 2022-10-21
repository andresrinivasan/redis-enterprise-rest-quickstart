# Redis Enterprise REST Quickstart

Assume current node is 10.128.0.2 and other nodes are 10.128.0.3 and 10.128.0.4, respectively.

*NOTE* Hardcoded IPs in JSON files too

## Create a Cluster

```sh
curl -k -X POST -H Content-Type:application/json -d @create-cluster.json https://localhost:9443/v1/bootstrap/create_cluster
```

## Verify the Cluster

```sh
curl -sk -u demo@redislabs.com:123456 -X GET -H Content-Type:application/json https://localhost:9443/v1/bootstrap | jq
```

## Join Nodes to the Cluster

*Note* The URL is connecting the REST endpoint on the node that is joining the cluster and the `cluster.nodes` key in the JSON is referencing the lead node that already exists in the cluster.

```sh
curl -k -X POST -H Content-Type:application/json -d @join-cluster.json https://10.128.0.3:9443/v1/bootstrap/join_cluster
curl -k -X POST -H Content-Type:application/json -d @join-cluster.json https://10.128.0.4:9443/v1/bootstrap/join_cluster
```

## List the Nodes in the Cluster

```sh
curl -sk -u demo@redislabs.com:123456 -X GET -H Content-Type:application/json https://localhost:9443/v1/nodes | jq
```

## Create a Sharded Cluster API Enabled Database

```sh
curl -k -u demo@redislabs.com:123456 -X POST -H Content-Type:application/json -d @create-sharded-oss-db.json https://localhost:9443/v1/bdbs
```

## List the Databases in the Cluster

```sh
curl -k -u demo@redislabs.com:123456 -X GET -H Content-Type:application/json https://localhost:9443/v1/bdbs | jq
```

## Delete a Database

```sh
curl -k -u demo@redislabs.com:123456 -X DELETE -H Content-Type:application/json https://localhost:9443/v1/bdbs/2
```
