# pop
PHP Oracle Pool Connectivity

### Preparation
```sh
root@server:~# su - oracle
oracle@server:~$ export ORACLE_SID=DBSIMPON
oracle@server:~$ sqlplus sys/SYSTEM@DBSIMPON as sysdba
```
Inside SQL Plus
```sh
SQL> conn / as sysdba
SQL> set linesize 121 col connection_pool format a30
SQL> SELECT connection_pool, maxsize FROM dba_cpool_info;
SQL> execute dbms_connection_pool.configure_pool(pool_name => 'SYS_DEFAULT_CONNECTION_POOL',minsize => 4,maxsize => 40,incrsize => 2,session_cached_cursors => 20,inactivity_timeout => 300,max_think_time => 600,max_use_session => 500000,max_lifetime_session => 86400);
SQL> execute dbms_connection_pool.start_pool();
```

### Reference
 1. http://psoug.org/reference/dbms_connection_pool.html