# Deploy single MongoDB instance for testing in Kubernetes

**NOTE:**  This deployment pattern should not be used in production. Strongly recommend a [StatefulSet for MongoDB Replica Sets](https://phoenixnap.com/kb/kubernetes-mongodb#deploy-a-replica-set).

```console
kubectl apply -k .
```

Verify pod is Ready then forward the port `27017` from the `mongodb-svc` to `localhost`

```
kubectl port-forward --address 0.0.0.0 svc/mongodb-svc 27017:27017 -n mongodb
```

From there we should be able to use `mongosh` client to connect to the MongoDB instance by connecting to `localhost`

```
mongosh -u admin -p Candy123
```

Once we are in the Mongo Shell, let's look for databases

```
test> show dbs
admin      100.00 KiB
asteroids   80.00 KiB
config      72.00 KiB
local       72.00 KiB
```

Now use the `asteroids` database

```
test> use asteroids
switched to db asteroids
```

Next we will look at the collections in this database

```
asteroids> show collections
asteroids
elements
```

Find all the documents in the `asteroids` collection

```
asteroids> db.asteroids.find()
[
  { _id: 1000, name: 'Bennu', elements: [ 100, 101, 108 ] },
  { _id: 1001, name: 'Ceres', elements: [ 106, 103, 108 ] },
  { _id: 1002, name: 'Pallas', elements: [ 103, 102, 105 ] },
  { _id: 1003, name: 'Juno', elements: [ 107, 106, 100 ] },
  { _id: 1004, name: 'Vesta', elements: [ 108, 101, 103 ] },
  { _id: 1005, name: 'Astraea', elements: [ 105, 101, 106 ] }
]
```