Create a Host Redis cluster with a couples of nodes


# 1st instance on port 6379
```
docker run -d  --network host --rm \
-v $PWD/node1/redis.conf:/usr/local/etc/redis/redis.conf \
--name redis-node1 redis redis-server /usr/local/etc/redis/redis.conf
```

# Second instance on port 6380
```
docker run -d --network host --rm \
-v $PWD/node2/redis.conf:/usr/local/etc/redis/redis.conf \
--name redis-node2 redis redis-server /usr/local/etc/redis/redis.conf
```

# 3rd instance on port 6381
```
docker run -d --network host --rm \
-v $PWD/node3/redis.conf:/usr/local/etc/redis/redis.conf \
--name redis-node3 redis redis-server /usr/local/etc/redis/redis.conf
```

# Operations on the cluster
```
docker run -it --rm --network host  redis \
redis-cli --cluster create  127.0.0.1:6379 127.0.0.1:6380 127.0.0.1:6381

docker run -it --rm --network host  redis redis-cli -h 127.0.0.1 -p 6379
```
