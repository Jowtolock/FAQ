# Windows 服务器端

> **\[warning\] 注意**
>
> 安装前需要保证服务器端与云锁云中心的443端口通信保持畅通，可以通过命令`telnet apiv3.yunsuo.com.cn 443`检查是否连通，连通则按照下面步骤进行安装；如不通则检查防火墙规则或云主机安全策略，将出站的443端口放开。PS：提示telnet未安装可通过百度查询安装方法。

访问[云锁官网](http://www.yunsuo.com.cn)，进入下载页面将Windows服务器端下载到服务器上。如有其它安全产品，需临时关闭其防护进行安装，安装完成后再开启防护。

下载完成后进行安装，在安装界面选择安装路径及云锁的监听端口，如不需要修改则以默认值进行安装。

![](../../.gitbook/assets/installW01.png)

安装过程中在安装网络层驱动时，会出现网络闪断几秒钟，安装完成后网络会自动恢复。

![](../../.gitbook/assets/installW02.png)

安装完成后会弹出加入云中心的页面，已经注册了云锁云中心账号，则输入账号和密码；如未注册则点击“立即注册”进行注册，注册成功后加入云中心；或“跳过”以后通过PC端将服务器添加到云中心进行管理。

![](../../.gitbook/assets/installW03.png)

![](../../.gitbook/assets/installW04.png)

由于云锁为了节省服务器端资源占用，采用了CS架构的方式进行管理。所以安装完成后没有界面，只在任务管理器中显示云锁进程，需安装[**PC端**](pc.md)进行管理。

![](../../.gitbook/assets/installW05.png)
