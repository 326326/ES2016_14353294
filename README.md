[TOC]



### 一.分布式操作的简单描述

​        分布式操作层（DOL）是一个是一个软件开发框架编程并行应用程序。劳工部允许指定的基础上计算的卡恩过程网络模型应用程序和功能的基础上的SystemC模拟引擎。此外，劳工部提供了一个基于XML的规范格式来描述在一个多处理器系统，包括绑定和映射并行应用程序的执行。

![picture1](https://cloud.githubusercontent.com/assets/22683831/19221438/633203ac-8e76-11e6-9205-4afbadb1d607.png)           				   <p align=“center”>嵌入式系统设计</p>

### 二.DOL安装笔记（如何安装DOL）

###### 1.安装一些必要的环境

$  sudo apt-get update

$  sudo apt-get install ant

$   sudo apt-get install openjdk-7-jdk

$  sudo apt-get install unzip

###### 2.解压文件

a)新建dol文件夹

$	mkdir dol

b)将dolethz.zip解压到 dol文件夹中

$	unzip dol_ethz.zip -d dol

![picture2](https://cloud.githubusercontent.com/assets/22683831/19221686/e787e9b0-8e7a-11e6-95e0-3b9773e84911.png)

dolethz.zip解压结果如图所示

c)解压systemc

$	tar -zxvf systemc-2.3.1.tgz

![picture3](https://cloud.githubusercontent.com/assets/22683831/19221729/5c063170-8e7b-11e6-9f3e-cffbfafd676c.jpg)

systemc解压结果如图所示

###### 3.编译systemc

a)解压后进入systemc-2.3.1的目录下

$	cd systemc-2.3.1

b)新建一个临时文件夹objdir

$	mkdir objdir

c)进入该文件夹objdir

$	cd objdir

d)运行configure(能根据系统的环境设置一下参数，用于编译)

$	../configure CXX=g++ --disable-async-updates

![picture4](https://cloud.githubusercontent.com/assets/22683831/19221786/7dd3b1aa-8e7c-11e6-9874-60cbc58287f4.jpg)

运行configure之后截图

e)编译

$	sudo make install

![picture5](https://cloud.githubusercontent.com/assets/22683831/19221799/f2239b4c-8e7c-11e6-9e8d-62ec180b6ac1.jpg)

​                                                                  编译后运行结果截图 

​                                                   ![picture6](https://cloud.githubusercontent.com/assets/22683831/19221806/257a84e2-8e7d-11e6-92c9-d817ae288c4f.png) 

​                                                                          当前路径截图

###### 4.编译dol

a)进入刚刚dol的文件夹

$	cd ../dol

b)修改build_zip.xml文件

找到下面这段话，就是说上面编译的systemc位置在哪里，
<property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）

![picture7](https://cloud.githubusercontent.com/assets/22683831/19221839/f23c9df8-8e7d-11e6-8255-71e4ada942dc.jpg)

​                                                                       修改结果如图

c)编译

$	ant -f build_zip.xml all

![picture8](https://cloud.githubusercontent.com/assets/22683831/19221853/31c9a0e2-8e7e-11e6-9c14-dae9575be45d.jpg)

​                                                                          编译结果如图

d)再编译

进入build/bin/mian路径下

$	cd build/bin/main

$	ant -f runexample.xml -Dnumber=1

![picture9](https://cloud.githubusercontent.com/assets/22683831/19221868/7054c0ee-8e7e-11e6-8e27-2e33ba3ca6ea.jpg)

编译成功结果如图

### 三实验问题及解决方案

###### 1.问题

a)在编译systemc的过程中，执行$  sudo make install的过程中很慢。

b)修改build_zip.xml文件后，第二次build一直失败。

###### 2.解决办法

a)对于执行$  sudo make install过程很慢，我们从Ubuntu Software Center里面更换别的下载地址，提高下载速度。

b)在修改build_zip.xml文件添加路径时，需要把最后的objdir单词删去，最后方可编译成功。

### 四.实验感想

​        本次实验虽然十分的简单，但是却花了我好长的时间，在DOL的安装过程中，特别是在编译修改build_zip.xml文件的过程中，我真的是心力交瘁。按照ppt上的修改步骤我不断地修改，不断地重新开始装DOL（我原以为是我前面安装出错了），可是最后在群上看到同学发的解决方法后，我无语了。因为这一切的错都来源于修改的路径，是因为最后多加了那个objdir，虽然我很生气，但是我对虚拟机的操作也更加熟悉了，所以总体上来说，我还是很高兴的！



































