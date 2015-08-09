# Redis Master/Slave Pair with 3 Sentinels

## Starting

``` bash
$ vagrant up
$ ansible-playbook -i hosts setup.yml -k
```

See also [Redis Sentinels](http://redis.io/topics/sentinel)

## Issues

If you destroy the machines and then provision new ones, you will need to delete the destroyed machines from your known_hosts file.