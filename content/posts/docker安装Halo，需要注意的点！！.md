---
title: "My First Post"
date: 2020-03-06T14:21:45+08:00
draft: false
toc: false
images:
tags: 
  - untagged
---

### docker install halo
今天，我使用docker安装halo，按照这个[教程](https://halo.run/archives/install-with-docker)来的。
*****
但是由于文档并没有介绍清楚使用mysql应该怎么做
我使用docker安装了mysql5.7。
```
docker pull mysql:5.7
```
可能会执行失败，多试几次即可。
然后执行
```
docker run -d -p 3306:3306 --name mymysql -e MYSQL_ROOT_PASSWORD=mimaxxx  mysql:5.7
```
接下来
```
docker run --rm -it -d --name halo -p 8090:8090  -v ~/.halo:/root/.halo ruibaby/halo

```
  发现并不能启动halo，于是在代码中查找日志所在位置
```
logging:
  level:
    run.halo.app: INFO
  file:
    path: ${user.home}/.halo/logs
```
在登陆远程服务器后，找到日志文件 spring.log。
发现错误如下
```
2020-03-04 13:00:47.220 ERROR 6 --- [main] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Exception during pool initialization.

com.mysql.cj.jdbc.exceptions.CommunicationsException: Communications link failure

The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
	at com.mysql.cj.jdbc.exceptions.SQLError.createCommunicationsException(SQLError.java:174) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:64) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.mysql.cj.jdbc.ConnectionImpl.createNewIO(ConnectionImpl.java:836) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.mysql.cj.jdbc.ConnectionImpl.<init>(ConnectionImpl.java:456) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.mysql.cj.jdbc.ConnectionImpl.getInstance(ConnectionImpl.java:246) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.mysql.cj.jdbc.NonRegisteringDriver.connect(NonRegisteringDriver.java:199) ~[mysql-connector-java-8.0.18.jar!/:8.0.18]
	at com.zaxxer.hikari.util.DriverDataSource.getConnection(DriverDataSource.java:138) ~[HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.pool.PoolBase.newConnection(PoolBase.java:353) ~[HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.pool.PoolBase.newPoolEntry(PoolBase.java:201) ~[HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.pool.HikariPool.createPoolEntry(HikariPool.java:473) [HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.pool.HikariPool.checkFailFast(HikariPool.java:562) [HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.pool.HikariPool.<init>(HikariPool.java:115) [HikariCP-3.4.1.jar!/:na]
	at com.zaxxer.hikari.HikariDataSource.getConnection(HikariDataSource.java:112) [HikariCP-3.4.1.jar!/:na]
	at org.hibernate.engine.jdbc.connections.internal.DatasourceConnectionProviderImpl.getConnection(DatasourceConnectionProviderImpl.java:122) [hibernate-core-5.4.8.Final.jar!/:5.4.8.Final]

```
经过各种查找后，有大佬说docker默认的网络模式是bridge，容器内127.0.0.1访问不到的，把网络模式改为跟宿主机相同就ok，并提供了启动halo的脚本
[解决方案](https://bbs.halo.run/d/112-docker-halo-mysql)
```
docker run --rm -it -d --net host --name halo-dev -p 8090:8090 -v ~/.halo:/root/.halo ruibaby/halo
```
经测试，可以启动了。
*****
感谢来访，本文到此结束
