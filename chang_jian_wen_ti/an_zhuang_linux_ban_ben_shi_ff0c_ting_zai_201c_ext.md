## 安装Linux版本时，停在“extract compression package”无法继续安装的问题 {#linux-extract-compression-package}

在安装云锁Linux版本时，安装运行到“extract compression package”无法继续安装（如下图）。主要是由于系统字符集设置导致的，此时将系统默认字符集临时改为C语言，再次执行安装即可。

1.  按“Ctrl + c”结束安装
2.  # export LC_ALL=C # 将系统语言环境临时转为C语言
3.  ./yunsuo_agent_...bit.bin # 再次安装云锁