

MONGODB REPLICA SET WITH AUTHENTICATION USING DOCKER CONTAINERS
===============================================================

This directory contains a mongodb replica set configuration environment using docker.
Optional authentication mechanism is explained below.


Quick start
-----------

### Step 1: Install Docker

[Install Docker][Docker-installation]


### Step 2: Install Docker Compose

[Install Docker Compose][Docker-compose-installation]


### Step 3: Create container directories

```sh
$ sudo mkdir -vp /srv/container/{mongo-rs-1,mongo-rs-2,mongo-rs-3}
```

### Step 4. Initiate replica set using 

```
rs.initiate(
	{
		_id: "rslocal", 
		members:[
		{ _id : 0, host : "localhost:27017"},
		{ _id : 1, host : "localhost:27018"},
		{ _id : 2, host : "localhost:27019"}
		]
	}
);
```

Optional. Activate authentication
---------------------------------

### Step 1. Connect to primary node
You can check which one using the following mongo command

```
rs.status()
```

### Step 2. Create an admin user and set his [roles][mongodb-roles]

```
db.createUser(
	{	
		user: "admin",
		pwd: "admin",
		roles: [{ role: "userAdminAnyDatabase", db: "admin"}]
	}
);
```

### Step 3. Stop replica set

```sh
$ docker-compose stop
```

### Step 4. Uncomment the following part
in docker-compose.yml file

```
# --auth --keyFile /data/db/mongodb-keyfile part
```

### Step 5. Startup replica set

```sh
$ docker-compose up -d
```

[Docker-installation]: https://docs.docker.com/engine/installation/
[Docker-compose-installation]: https://docs.docker.com/compose/install/
[mongodb-roles]: https://docs.mongodb.com/manual/core/security-built-in-roles/
