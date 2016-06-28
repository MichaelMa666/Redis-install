# Redis-install
Install Redis on Redhat 6.5

1.Preparation 

Redhat-6.5

redis-3.0.7.tar.gz download from : http://download.redis.io/releases/redis-3.0.7.tar.gz

2.Compile

$tar -zxcf redis-3.0.7.tar.gz

$cd redis-3.0.7/src

$make

$...

$sudo make install

3.move files

to create two directory to manage these files

$mkdir -p /usr/local/redis/bin

$mkdir -p /usr/local/redis/etc

then copy the file

$cd redis-3.0.7

$ls

00-RELEASENOTES  COPYING  Makefile   redis.conf        sentinel.conf  utils

BUGS             deps     MANIFESTO  runtest           src

CONTRIBUTING     INSTALL  README     runtest-sentinel  tests

$mv redis.conf /usr/local/redis/etc

$cd src

$mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-dump redis-cli redis-sentinel redis-server /usr/local/redis/bin/

4.Start Redis service

$cd /usr/loacl/redis/bin

$ls

mkreleasehdr.sh  redis-check-aof   redis-cli       redis-server

redis-benchmark  redis-check-dump  redis-sentinel

$./redis-server

/*********there will show something like this*******************/

Redis 3.0.7 (00000000/0) 64 bit

Running in standalone mode

Port: 6379

PID: 6284

http://redis.io

/****************************************************************/

Now the redis is running at the front desk. We need to let it run on the background.So wo shoould edit the configure file.

$gedit /usr/local/redis/etc/redis.conf

then search "daemonize" and modify the "no" to "yes"

save and exit.

We can start redis by configure file.

$./redis-server /usr/local/redis/etc/redis.conf

$ps -ef | grep redis

root      6349     1  0 20:33 ?        00:00:00 ./redis-server *:6379                    

root      6353 30683  0 20:33 pts/0    00:00:00 grep redis

We can see the redis process is running on the background.

5.sign in client

$ /usr/local/redis/bin/redis-cli

there will show 

$127.0.0.1:6379>

$127.0.0.1:6379>

$127.0.0.1:6379>

set key and value ,delete the key :

127.0.0.1:6379> set hello world

OK

127.0.0.1:6379> get hello

"world"

127.0.0.1:6379> del hello

(integer) 1

127.0.0.1:6379> get hello

(nil)

127.0.0.1:6379>

6.exit and close the service

$exit

$netstat -tunpl | grep 6379

tcp        0      0 0.0.0.0:6379                0.0.0.0:*                   LISTEN      6349/./redis-server

tcp        0      0 :::6379                     :::*                        LISTEN      6349/./redis-server

$pkill redis-server

$netstat -tunpl | grep 6379

$

It's ok...




