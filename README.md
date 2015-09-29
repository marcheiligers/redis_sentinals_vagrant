# Redis Master/Slave Pair with 3 Sentinels

## Provisioning

``` bash
$ vagrant up
$ ansible-playbook -i hosts setup.yml -k
```

This will also set redis2 as a slaveof redis1 and start all redis and sentinels.

See also [Redis Sentinels](http://redis.io/topics/sentinel)

## Start up

``` bash
$ ansible-playbook -i hosts startup.yml -k
```

Will just start the redis and sentinels again (like after a `vagrant halt`)

## Some commands to play with

``` bash
ssh vagrant@192.168.56.201 sudo /opt/redis/redis-server /opt/redis/redis.conf
ssh vagrant@192.168.56.202 sudo /opt/redis/redis-server /opt/redis/redis.conf

redis-cli -h 192.168.56.201 flushall
redis-cli -h 192.168.56.202 flushall

redis-cli -h 192.168.56.201 client pause 10000
redis-cli -h 192.168.56.203 -p 26379 sentinel failover redis
redis-cli -h 192.168.56.201 shutdown save
```

## Issues

If you destroy the machines and then provision new ones, you will need to delete the destroyed machines from your known_hosts file.