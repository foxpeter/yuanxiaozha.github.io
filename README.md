### Welcome to Yuanxiaozha Blog

大家好，我是猿小札。 本频道免费分享最新最快科学上网方法，破解VPN，科学上网翻墙方法，实用教程，实用电脑手机APP。 记得订阅我哦！并且打开小铃铛哦！多多点赞，评论，我会保持更新！ 更多内容请看：https://www.youtube.com/channel/UCLyUXIEt4vuyjxY6RoL36kQ 



免责声明： 本频道提供的任何资源教程，仅仅是技术交流，请在24小时内删除，切勿传播。假如你使用了任何本频道提供的资源教程，请遵守所在国的法律法规，切勿用于涉及政治宗教色情犯罪等领域发布违法言论，一切违法后果请自负。

Oracle Cloud甲骨文云初始配置

用Putty登陆入，用户名是opc或ubuntu
切换到root角色
sudo -i

安装相关依赖
CentOS如下
yum -y install wget
yum update -y && yum install curl -y
Ubuntu如下
apt-get install wget
apt-get update -y && apt-get install curl -y

删除、关闭、打开各自系统的无用附件、防火墙、端口及规则
CentOS系统
删除多余附件
systemctl stop oracle-cloud-agent
systemctl disable oracle-cloud-agent
systemctl stop oracle-cloud-agent-updater
systemctl disable oracle-cloud-agent-updater
停止firewall
systemctl stop firewalld.service
禁止firewall开机启动
systemctl disable firewalld.service

Ubuntu系统
开放所有端口
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
Ubuntu镜像默认设置了Iptable规则，关闭它
apt-get purge netfilter-persistent
reboot
或者强制删除
rm -rf /etc/iptables &amp;&amp; reboot
Oracle Cloud甲骨文云开启Socks5代理和免费更换IP教程
CentOS下使用Gost搭建一个快速简单的Socks5代理通道
说明:
Socks5属于明文代理，不要用于魔法上网，否则会被阻断端口，可用于正常的跳板使用
比如SSH转发加速国外VPS的连接速度，特别是一些延迟高或者丢包高的VPS
使用Socks5转发后SSH就可以快速稳定的连接了，解决高丢包SSH断开的问题
特性:
多端口监听
可设置转发代理，支持多级转发(代理链)
支持标准HTTP/HTTPS/HTTP2/SOCKS4(A)/SOCKS5代理协议
Web代理支持探测防御
支持多种隧道类型
SOCKS5代理支持TLS协商加密
Tunnel UDP over TCP
TCP/UDP透明代理
本地/远程TCP/UDP端口转发
支持Shadowsocks(TCP/UDP)协议
支持SNI代理
权限控制
负载均衡
路由控制
DNS解析和代理
TUN/TAP设备
搭建:
使用opc登入后，先sudo -i获取root权限
下载安装
wget "https://github.com/ginuerzh/gost/releases/download/v2.5-rc2/gost_2.5-rc2_linux_amd64.tar.gz"

tar -zxvf gost_2.5-rc2_linux_amd64.tar.gz

mv gost_2.5-rc2_linux_amd64/gost /usr/bin/gost

chmod +x /usr/bin/gost
开启代理
## 其中的 “账号” “密码” “端口” 自行修改

nohup gost -L 账号:密码@:端口 socks5://:端口 > /dev/null 2>&1 &
说明：使用的是nohup命令挂载到后台运行，重启后失效，再次挂载即可重新使用；

关闭代理
kill -9 $(ps aux | grep "gost" | sed '/grep/d' | awk '{print $2}')
编辑/etc/gost.json文件可修改配置数据
如果使用宝塔面板需要在面板放行设置的端口
最后客户端使用Proxifier连接上述Socks5的端口，就可以实现全局应用都使用Oracle Cloud的IP了.


[refer](https://zhuanlan.zhihu.com/p/352736372?)


### Blog

[2021甲骨文云Oracle Cloud搭建V2ray/SS](./2021甲骨文云Oracle Cloud搭建V2ray和SS.md)

[2021甲骨文云Oracle Cloud搭建trojan](./2021甲骨文云Oracle Cloud搭建trojan.md)

[2021使用github搭建免费博客](./2021使用github进行免费博客搭建.md)

### Support or Contact

[Telegram](https://t.me/yuanxiaozha)

[Youtube](https://www.youtube.com/channel/UCLyUXIEt4vuyjxY6RoL36kQ)

