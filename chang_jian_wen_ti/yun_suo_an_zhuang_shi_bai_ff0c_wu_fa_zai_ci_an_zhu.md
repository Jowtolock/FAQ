## 云锁安装失败，无法再次安装或卸载失败时的解决方法

1.  首次安装云锁，需判断是否安装其它类似安全软件，关闭注册表相关保护进行安装
2.  曾经安装过云锁，则按照如下步骤操作
3.  先从添加删除程序里卸载云锁
4.  然后cmd下执行
<br>sc stop yunsuoagent
<br>sc delete yunsuoagent
<br>sc stop yunsuodaemon
<br>sc delete yunsuodaemon
<br>sc delete resguard
<br>sc delete resguard2
<br>sc delete secmodel
5.  执行后重启操作系统，然后再次安装云锁