# ROS简介

机器人操作系统（ROS, Robot Operating System）是一个用于机器人软件开发的开源框架。它提供了操作系统的服务，包括硬件抽象、底层设备控制、常用功能的实现、进程间的消息传递以及包管理。ROS还支持分布式计算，使得多个计算节点可以无缝协作。

# 教程链接

[官方教程](https://wiki.ros.org/cn/ROS/Tutorials)
[conda安装教程](https://blog.csdn.net/m0_63834988/article/details/131867701)
[conda安装建议](https://blog.csdn.net/weixin_44566432/article/details/135123700)

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
