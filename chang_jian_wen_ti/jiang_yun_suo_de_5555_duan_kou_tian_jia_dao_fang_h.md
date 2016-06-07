## 将云锁的5555端口添加到防火墙的方法 {#5555}

Windows：

1.  打开防火墙高级设置
2.  “入站规则”处选择“新建规则”，将5555端口添加到防火墙

Linux：

1.  编辑iptables文件，vi /etc/sysconfig/iptablse，添加如图所示规则，保存退出

-A INPUT –p tcp –m tcp –dprot 5555 –j ACCEPT

-A INPUT –p udp –m udp –dprot 5555 –j ACCEPT

-A OUTPUT –p tcp –m tcp –sprot 5555 –j ACCEPT

-A OUTPUT –p udp –m udp –sprot 5555 –j ACCEPT

1.  重启防火墙iptables；service iptables restart