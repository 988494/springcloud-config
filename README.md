# Springcloud config 配置中心（个人觉得用得少，没有图形化界面，阿波罗功能更人性化-推荐使用阿波罗）
## 配置中心得选择有主流得三种
  Springcloud config<br>
  Apollp(阿波罗)<br>
  zookeeper(唯品会就是用得zookeeper)<br>
## 配置：
	windows中配置host文件中的域名解析，在C:\Windows\System32\drivers\etc\HOSTS中添加如下配置<br>
	127.0.0.1 eureka7001.com<br>
	127.0.0.1 eureka7002.com<br>
	127.0.0.1 eureka7003.com<br>
  127.0.0.1 myzuul.com<br>
## 数据库脚本：
```clouddb01```:<br>
DROP TABLE IF EXISTS `dept`;<br>
CREATE TABLE `dept` (<br>
  `deptno` bigint(20) NOT NULL AUTO_INCREMENT,<br>
  `dname` varchar(60) DEFAULT NULL,<br>
  `db_source` varchar(60) DEFAULT NULL,<br>
  PRIMARY KEY (`deptno`)<br>
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;<br>
<br><br><br>

```clouddb02```:<br>
DROP TABLE IF EXISTS `dept`;<br>
CREATE TABLE `dept` (<br>
  `deptno` bigint(20) NOT NULL AUTO_INCREMENT,<br>
  `dname` varchar(60) DEFAULT NULL,<br>
  `db_source` varchar(60) DEFAULT NULL,<br>
  PRIMARY KEY (`deptno`)<br>
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;<br>
<br><br><br>

```clouddb03```:
DROP TABLE IF EXISTS `dept`;<br>
CREATE TABLE `dept` (<br>
  `deptno` bigint(20) NOT NULL AUTO_INCREMENT,<br>
  `dname` varchar(60) DEFAULT NULL,<br>
  `db_source` varchar(60) DEFAULT NULL,<br>
  PRIMARY KEY (`deptno`)<br>
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;<br>
<br><br><br>



## 列子1--config server与github配置文件连通了
## 启动顺序：<br>
	1.启动：microservicecloud-config-3344<br>
	其中microservicecloud为所有服模块的父工程，microservicecloud-api是公共模块<br>
	其他微服务不用管<br>
	<br><br>
## 结果呈现：
	访问:<br>
    先访问： http://localhost:3344/application-dev.yml<br>
    再访问：http://localhost:3344/application-test.yml显示得配置信息不同，则表示成功了！！！<br>
    <br><br>
    
## 列子2--config server与github配置文件连通+eureka、服务提供者配置文件用github的
## 启动顺序：
	1.启动：microservicecloud-config-3344、microservicecloud-config-eureka-client-7001、microservicecloud-config-dept-client-8001<br>
	其中microservicecloud为所有服模块的父工程，microservicecloud-api是公共模块<br>
	其他微服务不用管<br>
	<br><br>
## 结果呈现：
    先访问：http://localhost:3344/microservicecloud-config-eureka-client-dev.yml<br>
    再访问：http://localhost:3344/microservicecloud-config-eureka-client-test.yml显示得配置信息不同，则表示config server与github配置<br>
    文件连通了<br>
    最后访问：http://localhost:8001/dept/list查看显示的结果!有则表示成功了！<br>
    <br><br><br>
    
    切换配置：更改microservicecloud-config-dept-client-8001中bootstrap.yml的profile: dev改为profile: test<br>
    然后访问http://localhost:8001/dept/list查看显示的结果，并且查看数据是否切换数据库了！则表示切换配置成功了！达到目的<br><br>
   
