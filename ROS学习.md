# ROS简介

机器人操作系统（ROS, Robot Operating System）是一个用于机器人软件开发的开源框架。它提供了操作系统的服务，包括硬件抽象、底层设备控制、常用功能的实现、进程间的消息传递以及包管理。ROS还支持分布式计算，使得多个计算节点可以无缝协作。

# 教程链接

[官方教程](https://wiki.ros.org/cn/ROS/Tutorials)
[conda安装教程](https://blog.csdn.net/m0_63834988/article/details/131867701)
[conda安装建议](https://blog.csdn.net/weixin_44566432/article/details/135123700)
[YAML命令行文档](https://wiki.ros.org/ROS/YAMLCommandLine)

# 学习简记

## 激活conda环境

```shell
cd /home/username/anaconda3/bin
. ./activate #第一个点代表source，第二个点代表当前目录
```

## ROS启动

可以将指令都添加到user目录下的.bashrc文件中

输入

```shell
sudo gedit ~/.bashrc
# 然后添加工作区的启动文件，比如：
source /opt/ros/noetic/setup.bash
```

## ROS软件包

/catkin_ws目录下有build,devel,src

**build**:是构建空间的默认位置，同时cmake和make也是在这里被调用来配置和构建你的软件包

**devel**:是开发空间的默认位置，在安装软件包之前，这里可以存放可执行文件和库

**src**:放软件包和软件包编译用的CMakeLists.txt的位置

## 常用ROS指令

```shell
rospack
roscd
rosls
```

需要启动的时候直接启动.bashrc中即可（不过需要先激活conda环境）

## ROS节点

```shell
roscore # 运行所有ROS程序前首先要运行的命令
rosnode # 显示当前正在运行的ROS节点信息
rosnode info [节点名称]
rosrun [package_name] [node_name]
rosrun [package_name] [node_rawname]:=[new_name] #改变软件包中节点名称
rosnode ping [node_name] #测试是否正常
```

rosout 用于收集和记录节点的调试输出（它本身也是一个节点）

## ROS话题
节点与节点之间通过一个ROS话题来相互通信,一个节点在话题上发布信息，另一个节点则订阅该话题以接收信息
### 呈现节点与节点之间的关系
使用rqt软件包中的rqt_graph呈现节点与节点之间的关系
```shell
rosrun rqt_graph rqt_graph
```
图中节点与节点之间是话题
### 获取话题信息
使用rostopic(通过rostopic -h获取相关信息)
```shell
rostopic type [topic] # 消息的大概(msg_type)
rosmsg show [msg_type] # 查看消息的详细信息
```
### 发布消息
rostopic pub可以把数据发布到当前某个正在广播的话题上
```shell
rostopic pub [topic] [msg_type] [args]
# etc
rostopic pub -1 /turtule1/cmd_vel geometry_msgs/Twist -- '[2.0,0.0,0.0]' '[0.0,0.0,1.8]'
# 解释其中的每个参数
rostopic pub 将消息发布到指定话题
-1 会让rostopic只发布一条消息，然后推出
/turtle1/cmd_vel 话题名称
geometry_msgs/Twist 发布话题时要用到的消息的类型
-- 这一选项（两个破折号）用来告诉选项解析器，表明之后的参数都不是选项
后面的参数采用YAML标记语言
rostopic pub /turtle1/cmd_vel geometry_msgs/Twist -r 1 -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, -1.8]'
-r [frequency] 以特定频率源源不断地发布命令
rostopic hz [topic] 报告数据发布的速率
```
### 显示信息
rosrun rqt_plot

## ROS服务
Services是节点之间通讯的另一种方式。服务允许节点发送一个请求并获得一个响应
```shell
rosservice list 获取服务列表
rosservice type [服务] 查看某种服务的类型
rosservice call [service] [arg]
rossrv 
```
### ROS参数服务器
参数服务器能够存储整型（integer）、浮点（float）、布尔（boolean）、字典（dictionaries）和列表（list）等数据类型。rosparam使用YAML标记语言的语法。一般而言，YAML的表述很自然：1是整型，1.0是浮点型，one是字符串，true是布尔型，[1, 2, 3]是整型组成的列表，{a: b, c: d}是字典
