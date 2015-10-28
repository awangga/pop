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
SQL> alter system set local_listener=’DEV’;
SQL> alter system register;
SQL> show parameter local_listener;
SQL> quit;

oracle@server:~$ lsnrctl services PROD
oracle@server:~$ ps -ef|grep n000
```

Tablespace expand
```sh
export ORACLE_HOME=/home/oracle/u01/app/oracle/product/11.2.0/dbhome_1
export ORACLE_SID=DBSIMPON
./sqlplus /nolog
SQL> conn SYSTEM as sysdba
SQL> select TABLESPACE_NAME, FILE_NAME, BYTES from DBA_DATA_FILES;
SQL> alter database datafile
     '/home/oracle/u01/app/oracle/oradata/DBSIMPON/system01.dbf'
     resize 1024M;
```


### Reference
 1. http://psoug.org/reference/dbms_connection_pool.html
 2. https://kkempf.wordpress.com/2011/07/29/oracle-database-resident-connection-pooling-drcp/
 3. http://psoug.org/snippet/TABLESPACE-List-tablespaces-files-allocated-and-free-space_852.htm