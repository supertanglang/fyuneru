任务列表
========

## v1.2(未确定)

[      ] 1. 在客户端上设立控制端口，以便开发web界面，查看UDP流量、延迟，管理开放情况

[      ] 2. 考虑一种控制协议，可以通过上一条所述方式控制服务器端程序

[      ] 3. 修改Readme中的语法错误

[      ] 4. 用图显示本地各端口的延时情况。

## v1.1

[ DONE ] 1. 重构虚拟网卡为一个类，用纯Python实现，删除了对python-pytun的依赖

[ DONE ] 2. 修改代理接口的协议，也许使用Unix Socket，改进握手的协议，将接口的
            性能统计（通过DataPacket的时刻）也加入。

[delete] 2.1 v1.1-using-unix-socket 分支，使用Unix Socket作为代理进程和主进程
             之间的通信方式。需要一种统一的IPC模块来完成任务。
             (由于UnixSocket的特性，准备放弃此特性，重写由UDP连接的IPC）

[ DONE ] 2.2 使用UDP构建IPC服务器类，并将对代理程序的配置转用IPC完成

[ DONE ] 3. 为Shadowsocks代理增加在服务器重启后也能自动恢复连接的机制（Bugfix）

[ DONE ] 4. 修改加密协议，将加密后的UDP数据包长度随机化
            此功能目前没有在代码中启用。

[ DONE ] 5. 编写基于XMPP的代理(使用xmpppy)

[ pend ] 6. 使用Python的logging模块来管理log输出。


## 已完成的改进

1. 在IP帧封包中加入发送时刻，使得客户端和服务器都可确定某个UDP端口（或者说某个
   代理机制）是否堵塞。
1. 检测是否有root权限及在启动TUN后放弃root权限
1. config.json 加入version键，判断config.json是否兼容于本版本的程序。
1. config.json 修改，直接对（服务器-客户机）端口对进行配置，并针对每个端口对传
   递具体代理程序的情况。
1. 将Debug输出改成彩色。

## 远期计划 或 对其他开发者的建议

下面列的改进是远期计划中的目标，当前并没有实际的编程实现。

1. 在服务器上使用账户管理：
    1. 可以自动更换通信的对称密钥，使用类似ZRTP的机制，或者传统的公钥体系完成
       认证
    1. 用一个服务器为多个虚拟网卡提供服务，将服务器变成虚拟局域网的路由器。在
       本条实现后，可以开发额外的项目，实现多个虚拟网卡组网，甚至基于局域网内
       UDP的无服务器音视频加密聊天。

2. （放弃）使用multiprocessing模块代替Unix Socket进行IPC
   （当前在v1.1-multiprocessing分支中进行开发）。
