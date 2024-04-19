# Atelier-MongoDB-en-Mode-Replica-Set


## Prérequis

- Docker installé 
- npm installé 
- Accès à internet


# - Étape 1 : Configuration de MongoDB en Mode Replica Set

```bash 
docker network create mongoCluster
```

```bash 
docker run -d --rm -p 27017:27017 --name mongo1 --network mongoCluster mongo:5 mongod --replSet myReplicaSet --bind_ip localhost,mongo1
```

```bash 
docker run -d --rm -p 27018:27017 --name mongo2 --network mongoCluster mongo:5 mongod --replSet myReplicaSet --bind_ip localhost,mongo2

docker run -d --rm -p 27019:27017 --name mongo3 --network mongoCluster mongo:5 mongod --replSet myReplicaSet --bind_ip localhost,mongo3
```

```bash 
docker exec -it mongo1 mongosh --eval "rs.initiate({
 _id: \"myReplicaSet\",
 members: [
   {_id: 0, host: \"mongo1\"},
   {_id: 1, host: \"mongo2\"},
   {_id: 2, host: \"mongo3\"}
 ]
})"
```

```bash 
docker exec -it mongo1 mongosh --eval "rs.status()"
```

# - Étape 2 : Génération de Fausses Données 

```bash 
npm run genFakeData
```


# - Étape 3: Manipulations via la CLI MongoDB

