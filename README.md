# HiveHadoopDockerComposeSetup

### Step-1 - Clone the repo:
```
git clone https://github.com/vishalsingh17/HiveHadoopDockerComposeSetup.git
```

### Step-2 - Change the directory to the folder:
```
cd HiveHadoopDockerComposeSetup
```

### Step-3 - Start all services:
```
docker-compose up
```

### Step-4 - Verify container status:
```
docker stats
```

### Step-5 - Get Started:
Log onto the Hive-server and create a sample database and hive table by executing the below command in a new terminal.
```
docker exec -it hive-server /bin/bash
```
Navigate to the employee directory on the hive-server container.
```
root@dc86b2b9e566:/opt# ls
hadoop-2.7.4  hive
root@dc86b2b9e566:/opt# cd ..
root@dc86b2b9e566:/# ls
bin  boot  dev employee  entrypoint.sh  etc  hadoop-data  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@dc86b2b9e566:/# cd employee/
```
Execute the employee_table.hql to create a new external hive table employee under a new database testdb.

```
root@dc86b2b9e566:/employee# hive -f employee_table.hql
```

Now, let’s add some data to this hive table. For that, simply push the employee.csv present in the employee directory on the hive-server into HDFS.

```
root@dc86b2b9e566:/employee# hadoop fs -put employee.csv hdfs://namenode:8020/user/hive/warehouse/testdb.db/employee
```

### Step-6 - Validate the setup:
On the hive-server, launch hive to verify the contents of the employee table.
```
root@df1ac619536c:/employee# hive
hive> show databases;
OK
default
testdb
Time taken: 2.363 seconds, Fetched: 2 row(s)
```
```
hive> use testdb;
OK
Time taken: 0.085 seconds
```

```
hive> select * from employee;
OK
1 Rudolf Bardin 30 cashier 100 New York 40000 5
2 Rob Trask 22 driver 100 New York 50000 4
3 Madie Nakamura 20 janitor 100 New York 30000 4
4 Alesha Huntley 40 cashier 101 Los Angeles 40000 10
5 Iva Moose 50 cashier 102 Phoenix 50000 20
Time taken: 4.237 seconds, Fetched: 5 row(s)
```
