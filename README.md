# minernat

ETH矿池代理中转程序`hellominer`的客户端，用于安装在矿机本地局域网，为所有矿机提供统一入口，上级对接`hellominer`的`ws`协议端口，建立加密伪装隧道。
采用Golang语言开发，性能稳定优异。支持安装为系统服务，开机自启动，支持进程守护运行，程序自动调整连接数限制。Telegram交流群 [点击加入](https://t.me/hellominer_group) 。

## 系统要求

- 系统类型：Linux: `Debian 9`及以后, `Centos 7`及以后, `Ubuntu 12`及以后。
- 一台局域网Linux机器，矿机可以访问到它。

## 安装方式

`重要提示：因为会安装为系统服务，自动调整系统ulimit连接数限制，所有安装方式都需要root账号权限。`

### Linux 安装

1. [linux 点击下载 linux-minernat.tar.gz](https://github.com/hellominer/minernat/raw/main/releases/linux-minernat.tar.gz) 。
2. 执行：`mkdir /etc/minernat`，创建安装目录。
3. 把文件`linux-minernat.tar.gz`放在目录`/etc/minernat`下面。
4. 执行：`cd /etc/minernat && tar zxfv linux-minernat.tar.gz && ./minernat install`
5. 修改配置文件`/etc/minernat/minernat.toml` ，配置`hellominer`端口，
假设你`hellominer`服务器IP是`122.123.0.1`,代理端口是`8888`，协议tls，那么配置文件里面的`hellominer`的值改成`tls://122.123.0.1:8888`。
6. 安装完毕，记得启动哟。启动命令：`systemctl start minernat`。
7. 中转端口，默认是：`15555`，矿机连接的就是这个端口，可以通过修改`/etc/minernat/minernat.toml`里面的配置`listen`修改这个端口。

具体程序的`启动`，`停止`，`重启`，`状态`命令如下：

1. 程序启动：`systemctl start minernat`
2. 程序停止：`systemctl stop minernat`
3. 程序重启：`systemctl restart minernat`
4. 程序状态：`systemctl status minernat`
5. 启动日志：`journalctl -u minernat -e`
6. 程序卸载：`/etc/minernat/minernat uninstall`

#### 更新程序

更新程序只需要把下载的文件压缩包，解压的二进制文件`minernat`覆盖掉`/etc/minernat/minernat`，然后重启程序即可，程序重启：`systemctl restart minernat`。


### windows 安装

1. [windows 点击下载 windows-minernat.tar.gz](https://github.com/hellominer/minernat/raw/main/releases/windows-minernat.tar.gz) 。
2. 新建：`d:\minernat`，创建安装目录。
3. 把文件`windows-minernat.tar.gz`放在目录`d:\minernat`下面。
4. 执行解压，得到：minernat.exe。
5. 打开命令提示符：输入：`d:`
6. `cd minernat`
7. `.\minernat.exe init`
8. 修改配置文件`d:\minernat\minernat.toml` ，配置`hellominer`端口，
   假设你`hellominer`服务器IP是`122.123.0.1`,`ws`端口是`8888`，那么配置文件里面的`hellominer`的值改成`ws://122.123.0.1:8888`。
9. 安装完毕，双击`minernat.exe`就启动了，不要关闭窗口。
10. 中转端口，默认是：`15555`，矿机连接的就是这个端口，可以通过修改`d:\minernat\minernat.toml`里面的配置`listen`修改这个端口。

### windows 安装为系统服务
1. [windows 点击下载 windows-minernat.tar.gz](https://github.com/hellominer/minernat/raw/main/releases/windows-minernat.tar.gz) 。
2. 新建：`d:\minernat`，创建安装目录。
3. 把文件`windows-minernat.tar.gz`放在目录`d:\minernat`下面。
4. 执行解压，得到：minernat.exe。
5. 打开命令提示符：输入：`d:`
6. `cd minernat`
7. 执行`.\minernat.exe install`，就把`minernat`安装为系统服务，开机自动启动。
8. 修改配置文件`d:\minernat\minernat.toml` ，配置`hellominer`端口，
   假设你`hellominer`服务器IP是`122.123.0.1`,`ws`端口是`8888`，那么配置文件里面的`hellominer`的值改成`ws://122.123.0.1:8888`。 
9. 安装完毕，记得启动哟。启动命令：`net start minernat`。
10. 中转端口，默认是：`15555`，矿机连接的就是这个端口，可以通过修改`d:\minernat\minernat.toml`里面的配置`listen`修改这个端口。

具体程序的`启动`，`停止`，`卸载`命令如下：

1. 程序启动：`net start minernat`
2. 程序停止：`net stop minernat`
3. 程序卸载：`d:\minernat\minernat.exe uninstall`

#### 更新程序

更新程序只需要把下载的文件压缩包，解压的二进制文件`minernat.exe`覆盖掉`d:\minernat\minernat.exe`，然后重启程序即可。


## 问题交流

如果您遇到使用问题，欢迎加入telegram交流群 [点击加入](https://t.me/hellominer_group) 寻求帮助。

## 更新日志

### v2.3
- 新增压缩传输数据支持，可以使用低的服务器带宽承载更多的矿机连接。

### v2.2
- 新增ws/wss自定义密码支持。

### v2.1
- 优化连接。
- 支持更多协议。

### v2.0
- 兼容协议也可以使用了。
- 可以通过代理连接hellominer了。
- 新增windows支持。

### v1.0
- 首发