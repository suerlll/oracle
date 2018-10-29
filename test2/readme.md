第一步
```SQL
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_view;
SQL> GRANT connect,resource,CREATE VIEW TO omg_view;
SQL> CREATE USER new_user IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
SQL> ALTER USER new_user QUOTA 50M ON users;
SQL> GRANT con_res_view TO new_user;
SQL> exit
```
第二步
```SQL
$ sqlplus new_user/123@pdborcl
SQL> show user;
SQL> CREATE TABLE mytable (id number,name varchar(50));
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
SQL> SELECT * FROM myview;
SQL> GRANT SELECT ON myview TO hr;
SQL>exit
```
第三步
```SQL
$ sqlplus hr / 123 @pdborcl 
SQL> SELECT * FROM new_user.myview;
SQL >exit
```
第四步
```SQL
$ sqlplus new_user/123@pdborcl
SQL>SELECT tablespace_name,FILE_NAME,BYTES/1024/1024 MB,MAXBYTES/1024/1024 MAX_MB,autoextensible FROM dba_data_files  WHERE  tablespace_name='USERS';
SQL>SELECT a.tablespace_name "表空间名",Total/1024/1024 "大小MB",
 free/1024/1024 "剩余MB",( total - free )/1024/1024 "使用MB",
 Round(( total - free )/ total,4)* 100 "使用率%"
 from (SELECT tablespace_name,Sum(bytes)free
        FROM   dba_free_space group  BY tablespace_name)a,
       (SELECT tablespace_name,Sum(bytes)total FROM dba_data_files
        group  BY tablespace_name)b
 where  a.tablespace_name = b.tablespace_name;
```
