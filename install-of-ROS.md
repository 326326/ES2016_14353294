[TOC]

# 安装ROS

### 一.设置sources.list

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

![1](https://cloud.githubusercontent.com/assets/22683831/20056898/7881d50c-a523-11e6-8067-885f962a78d7.jpg)

结果截图如上

### 二.设置密钥

```
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
```

### 三.安装

###### 1.确保Debian包索引是最新的

```
sudo apt-get update
```

###### 2.设置默认配置

```
sudo apt-get install ros-jade-desktop-full
```

###### 3.查找可用的软件包

```
apt-cache search ros-jade
```

![2](https://cloud.githubusercontent.com/assets/22683831/20056900/7b88104a-a523-11e6-8fd0-69a4a1e69c89.jpg)

结果截图如上

###### 4.初始化ROS

```
sudo rosdep init
```

![3](https://cloud.githubusercontent.com/assets/22683831/20056905/7dcb2d74-a523-11e6-88d6-83f835ede21f.jpg)

截图结果如上

###### 5.更新rosdep

```
rosdep update
```

![4](https://cloud.githubusercontent.com/assets/22683831/20056912/81145e06-a523-11e6-9495-35f9b70d58d0.jpg)

截图结果如上

###### 6.配置环境变量

```
echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

###### 7.安装rosinstall

```
sudo apt-get install python-rosinstall
```

![5](https://cloud.githubusercontent.com/assets/22683831/20056913/8414cb36-a523-11e6-8af5-52904feb8cc9.jpg)

结果截图如上

### 四.实验问题与解决方案

###### 问题：

1.在初始ROS变量时，经常会报如下错误：

![r70f lltyupc ys 2sbwru](https://cloud.githubusercontent.com/assets/22683831/20057394/3927c8f0-a526-11e6-96b3-15a8daa84965.png)

######  解决方法：

 1.在输入初始化命令前，首先输入如下命令即可解决该问题：

 $ sudo rm -rf /etc/ros/rosdep/sources.list.d/*

### 五.实验感想

​    在本次试验过程中，问题虽然不多，但是都相当难以解决，我们必须阅读大量的资料从网上方可找出解决问题的办法，所以我们在实验安装过程中对ROS有了进一步的了解，这应该就是我们在这次实验中的最大收获。











