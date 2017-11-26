# Cluster With Docker

<https://hub.docker.com/r/mysql/mysql-cluster/>

## Master-Master

<https://vnextcoder.wordpress.com/2016/09/19/mysql-master-master-replication-setup-on-docker/>

### Prepare the configurations

~/server1/conf.d/server1.cnf

```
[mysqld]
 server-id = 101
 log_bin = /var/log/mysql/mysql-bin.log
 binlog_do_db = mydata
 bind-address = 0.0.0.0 # make sure to bind it to all IPs, else mysql listens on 127.0.0.1
 character_set_server = utf8
 collation_server = utf8_general_ci
 
[mysql]
 default_character_set = utf8
```

~/server1/backup/initdb.sql

```
use mysql;
create user 'replicator'@'%' identified by 'repl1234or';
grant replication slave on *.* to 'replicator'@'%';
# do note that the replicator permission cannot be granted on single database. 
FLUSH PRIVILEGES;
SHOW MASTER STATUS;
SHOW VARIABLES LIKE 'server_id';
```

~/server2/conf.d/server2.cnf

```
[mysqld]
server-id = 102 # Remember this is only Integer per official documentation
log_bin = /var/log/mysql/mysql-bin.log
binlog_do_db = mydata
bind-address = 0.0.0.0 # make sure to bind it to all IPs, else mysql listens on 127.0.0.1
character_set_server = utf8
collation_server = utf8_general_ci
[mysql]
default_character_set = utf8
```

~/server2/backup/initdb.sql

```
use mysql;
create user 'replicator'@'%' identified by 'repl1234or';
grant replication slave on *.* to 'replicator'@'%'; 
# do note that the replicator permission cannot be granted on single database. 
FLUSH PRIVILEGES;
SHOW MASTER STATUS;
SHOW VARIABLES LIKE 'server_id';
```


### Create Network

```
docker network create cluster --subnet=192.168.0.0/16
```

### Run Docker Container

mysql-server1:

```
docker run --name server1 --net=cluster -e MYSQL_ROOT_PASSWORD=mysql1pass -e MYSQL_DATABASE=mydata -dit -p 33061:3306 -v /Users/zhouleibo/var.docker/mysql/server1/conf.d:/etc/mysql/mysql.conf.d/   -v /Users/zhouleibo/var.docker/mysql/server1/data:/var/lib/mysql -v /Users/zhouleibo/var.docker/mysql/server1/log:/var/log/mysql -v /Users/zhouleibo/var.docker/mysql/server1/backup:/backup -h  server1 mysql
```

mysql-server2:

```
docker run --name server2  --net=cluster -e MYSQL_ROOT_PASSWORD=mysql2pass -e MYSQL_DATABASE=mydata -dit -p 33062:3306 -v /Users/zhouleibo/var.docker/mysql/server2/conf.d:/etc/mysql/mysql.conf.d/   -v /Users/zhouleibo/var.docker/mysql/server2/data:/var/lib/mysql -v /Users/zhouleibo/var.docker/mysql/server2/log:/var/log/mysql -v /Users/zhouleibo/var.docker/mysql/server2/backup:/backup -h  server2 mysql
```

### Initialize

```
docker exec -ti server1 sh -c "mysql -uroot -p"

source /backup/initdb.sql
```

```
docker exec -ti server2 sh -c "mysql -uroot -p"

source /backup/initdb.sql
```

### Setup the Replication source for both nodes

```
docker exec -ti server2 sh -c "mysql -uroot -p"

stop slave;

CHANGE MASTER TO MASTER_HOST = 'server1', MASTER_USER = 'replicator', MASTER_PASSWORD = 'repl1234or', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 1;

start slave;

show slave status;
```

```
docker exec -ti server1 sh -c "mysql -uroot -p"

stop slave;

CHANGE MASTER TO MASTER_HOST = 'server2', MASTER_USER = 'replicator', MASTER_PASSWORD = 'repl1234or', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 1;

start slave;

show slave status;
```

