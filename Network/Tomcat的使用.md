# Tomcat的使用
---

## 修改默认主页
简单粗暴的方式：
```
删掉tomcat下原有Root文件夹，将自己的项目更名为Root
```

假设想要修改webapps/xwiki8项目为网站的默认目录：
* 修改conf/server.xml
在server.xml文件中，有一段如下：
``` xml
……
<engine name="Catalina" defaultHost="localhost">
<host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true" xmlValidation="false" xmlNamespaceAware="false">
……
<host>
</engine>
……
```
在<host></host>标签之间添加上：
``` xml
<Context path="" docBase="xwiki8" debug="0" reloadable="true" />
```

* 修改conf/web.xml
在web.xml文件中，有一段如下：
``` xml
<welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
</welcome-file-list>
``` 

增加一行<welcome-file/>：
``` xml
<welcome-file>web.xml</welcome-file>
```

* 更该端口
将port="8080"改成想要的端口
``` xml
<Connector port="8080" maxThreads="150" minSpareThreads="25" maxSpareThreads="75" enableLookups="false" redirectPort="8443" acceptCount="100" debug="0" connectionTimeout="20000" disableUploadTimeout="true" /> 
```