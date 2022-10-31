MySQL User-defined function (UDF) for HTTP GET/POST
==========

MySQL User-defined function (UDF) for HTTP REST

**Note:** It is a fork repository. Original Website is below.  
http://code.google.com/p/mysql-udf-http

This fork is set up so http_post sends application/json instead of application/x-www-form-urlencoded, which you can send with MySQL's built-in JSON_OBJECT or JSON_ARRAY functions.

## Overview

| HTTP Method | CRUD Action |      Description       |
|-------------|-------------|------------------------|
| POST        |  CREATE     |  Create a new resource |
| GET         |  READ       |  Read a resource       |
| PUT         |  UPDATE     |  Update a resource     |
| DELETE      |  DELETE     |  Delete a resource     |

Support MySQL version 5.1.x and 5.5.x on Linux systems.

## User Guide

### 0. Prepare

make sure these depandencies are installed.

* mysql server
* mysql_config command
* development tools

For Debian, like this.

```
apt-get install mysql-server
apt-get install make
apt-get install gcc
apt-get install libmysqlclient-dev
apt-get install pkg-config
apt-get install libcurl4-gnutls-dev
```

### 1. Install on Linux

This sample is written for "/usr/bin/mysql/" is your MySQL install path.

```
wget https://github.com/AfifAhmad/mysql-udf-http/archive/refs/heads/master.zip
unzip master.zip -d master
cd master/mysql-udf-http-master/
./configure --prefix=/usr/ --with-mysql=/usr/bin/mysql_config
make && make install
cd ../
```

### 3. Create the UDF function in the MySQL console

```
mysql>

create function http_get returns string soname 'mysql-udf-http.so';
create function http_post returns string soname 'mysql-udf-http.so';
create function http_put returns string soname 'mysql-udf-http.so';
create function http_delete returns string soname 'mysql-udf-http.so';
```

### 4. Usage

#### Description:

```
mysql>
SELECT http_get('<url>');
SELECT http_post('<url>', JSON_OBJECT('<data>','<value>'));
SELECT http_put('<url>');
SELECT http_delete('<url>');
```

#### Example (A):

```
mysql>

select http_post("https://httpbin.org/post",  JSON_OBJECT('id', 87, 'name', 'carrot'));
```

### 5. How to drop the UDF function

```
mysql>

drop function http_get;
drop function http_post;
drop function http_put;
drop function http_delete;
```



## License

This is free software, and you are welcome to modify and redistribute it under the New BSD License.
