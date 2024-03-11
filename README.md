## Run the redis and redis-cli
1. Start the redis container
```bash
docker-compose up -d
```

2. Connect to the redis container via cli
```bash
docker run -it --rm --network redis-network redis:poc redis-cli -h redis-container
```

3. Remove docker container and associated volume
```bash
docker-compose down -v
```

4. Clean everything
```bash
docker-compose down -v; docker rmi redis:poc
```
