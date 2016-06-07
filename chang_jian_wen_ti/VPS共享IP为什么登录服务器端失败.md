## VPS共享IP为什么登录服务器端失败？

&emsp;&emsp;因为云锁的PC是默认通过5555端口连接服务器端，登录时需要在服务器端将端口号改为VPS开放的端口号（图1）或者将VPS内部端口5555映射到任意外部端口（图2），然后通过IP:52035的方式连接云锁。
<center>![](/assets/云锁监听端口.png)
<center>图 1
<center>![](/assets/端口映射.png)
<center>图 2

&emsp;&emsp;如果依旧不能登录，尝试在防火墙的入站规则将外部端口加为白名单。
<center>![](/assets/添加防火墙.png)