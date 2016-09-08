####  网站性能监控下为什么多了其它的域名？
&emsp;&emsp;这个首先要从正常访客使用浏览器访问一个网站的域名说起，假如你的域名是www.yunsuo.com.cn,那么正常访客提交的HTTP请求大概就是这样滴
<pre>GET /index.htm HTTP/1.1
Host: www.yunsuo.com.cn
Content-Type: text/html</pre>
&emsp;&emsp;然后连接 www.yunsuo.com.cn 指向的IP地址，发送这段字符串，浏览器就可以接收数据了。

&emsp;&emsp;云锁按照网站统计流量，正是以这个Host字段中的值来区分不同的站的。
在网站性能监控数据里出现不属于自己的网站，正是由于别人使用了自己定义的Host字段所致，话说别人为啥要这么做呢

1. 恶意解析，将大流量网站的域名解析到你的服务器上，造成网络拥堵。

2. 工具探测，假设我现在想知道百度服务器的真正的IP地址，但是我只知道百度的域名，咋办呢，暴力搜索。

用程序这样提交数据
<pre>GET /index.htm HTTP/1.1
Host: www.baidu.com
Content-Type: text/html</pre>
&emsp;&emsp;程序会在一个循环里连接所有可能的IP地址来探测，当对端服务器返回了正常的百度首页地址，则表示找到了他的IP地址。

&emsp;&emsp;一般来讲，这样的数据在网站性能监控里会很少，一天下来PV也没几次。如果发现一个不属于自己的网站，一天下来PV很高，那可能是遇到了第一种情况或是碰到了攻击行为。