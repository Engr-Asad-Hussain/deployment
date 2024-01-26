## MongoDB Deployment
Run the ```compose.yaml``` docker-compose file.
```bash
$ docker-compose --file "D:\protected_resources\deployment\mariadb.yaml" up -d
```

Stop and destroy the remove Docker container.
```bash
$ docker-compose --file "D:\protected_resources\deployment\mariadb.yaml" down
```

Note:
`--file` requires the path of your `compose.yaml` file. You can provide related or non-related file path in --file argument in the quotes.

## Few commands of MongoDB
`docker-compose exec -it mongo bash`
```sh
mongosh
>> use admin
>> db.auth("username", "password")
>> show dbs / show databases
>> show collections / show tables
>> show users
>> show roles
```
Other useful commands:
```sh
>> use products # product is the name of database
>> db.products.find() # list all the objects in products
>> db.products.insertOne({name: '4G System', price: 280, rating: 4.5, company: 'Router'})
>> db.products.findOneAndUpdate({_id: ObjectId('65b22eaa68401bcef15c8e07')}, {$set: {featured: true}})
```