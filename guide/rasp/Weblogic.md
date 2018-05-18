# Weblogic安装
>**[info] 建议
>
>安装前重启一次Web的服务，确保业务重启后可以正常运行，然后再安装云锁防护模块；同时将要修改的配置文件进行备份。

**Web容器使用的Java（jdk或jre）的版本需 1.6 及以上。**

- [Windows安装说明](#Windows)
- [Linux安装说明](#Linux)

## Windows

1）拷贝`jspAgent`目录到`%DOMAIN_HOME%`下。

2）修改`%DOMAIN_HOME%\bin\startWebLogic.cmd`， 定位到
`set JAVA_OPTIONS=%SAVE_JAVA_OPTIONS%`， 在其下追加一行：`set JAVA_OPTIONS=-javaagent:%DOMAIN_HOME%\jspAgent\JSPAgent.jar %JAVA_OPTIONS%`

![](/assets/WeblogicW.png)

3）重启 WebLogic。

## Linux

1）首先获取startWebLogic.sh位置：
```
    # ps -elf | grep startWebLogic.sh
    /bin/sh ./root/wls12130/user_projects/domains/mydomain/startWebLogic.sh
    /bin/sh /root/wls12130/user_projects/domains/mydomain/bin/startWebLogic.sh
```
![](/assets/WeblogicL01.png)

由此确定工作目录为：`DOMAIN_HOME =/root/wls12130/user_projects/domains/mydomain`

2）拷贝`jspAgent`目录到`${DOMAIN_HOME}`下。

3）修改`${DOMAIN_HOME}/bin/startWebLogic.sh`中JAVA启动参数，定位到 `JAVA_OPTIONS="${SAVE_JAVA_OPTIONS}`，其下追加一行：`JAVA_OPTIONS="-javaagent:${DOMAIN_HOME}/jspAgent/JSPAgent.jar ${JAVA_OPTIONS}"`

![](/assets/WeblogicL02.png)

4）重启weblogic。

