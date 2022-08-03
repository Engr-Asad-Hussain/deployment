# Deployment Service
Protected Services (PS) Backend (BE) template - Shows good practices. 
A REST API to ......

## Contents
- [MariaDB Deployment](#mariadb-deployment)
- [Login Credentials](#login-credentials)


## MariaDB Deployment
- Run the ```mariadb.yaml``` docker-compose file.
```bash
$ docker-compose --file "D:\protected_resources\deployment\mariadb.yaml" up -d
```

- Stop and destroy the creat docker container.
```bash
$ docker-compose --file "D:\protected_resources\deployment\mariadb.yaml" down
```

## Login Credentials
- The credentials for the normal user is:
```{"username": "admin", "password": "auxin123"}```.
This user don't have permissions to do certain actions, in order to give permissions login as root user and give permissions.

- The credentials for the root user, having all the privileges:
```{"username": "root", "password": "root"}```