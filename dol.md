[TOC]

## Lab2：DOL实例分析&编程

#### 一.修改example2，让3个square模块变成2个，tips：修改xml的iterator

###### 1)*.dol截图如下：

 原始dol截图：![image](https://cloud.githubusercontent.com/assets/22683831/19855063/773a25d0-9fad-11e6-959f-0e3d7a93fd8f.png)

修改后的dol截图 

 ![image](https://cloud.githubusercontent.com/assets/22683831/19855045/4cd0c088-9fad-11e6-9cc2-08a4a34bcbc5.png)

![dol](https://cloud.githubusercontent.com/assets/22683831/19846876/bf130f8c-9f7d-11e6-9d50-599f16adf6c4.jpg)

​        如上图所示：在dol截图中generator为生产者模块，square_0和square_1为两个平方模块，consumer为消费者模块，C2_0、C2_1为两条线，即连接各模块的通道（各个通道必须连接两个模块）。

###### 2）各个模块的代码分析如下：

​        generation模块：

​                                               ![generator_init](https://cloud.githubusercontent.com/assets/22683831/19847182/0054f094-9f80-11e6-89b8-68955cc24ab8.png)

​        如上图所示：该代码为generator的初始化代码，首先该段代码设置了当前的位置为0，设置了生产者的长度为length。

​                         ![fire](https://cloud.githubusercontent.com/assets/22683831/19847287/d64e698c-9f80-11e6-92c4-f57943df90ec.png)

​        如上图所示：该段代码首先用local指针指向.h文件的_local_states结构，然后是在fire信号产生函数中，通过比较当前位置与生产者的长度，从而将x进行输出或者销毁。

​        square模块：

​              ![square](https://cloud.githubusercontent.com/assets/22683831/19847478/2a59ef14-9f82-11e6-96ae-8ce3a34f0f97.jpg)

​        如上图所示：在square模块中，我们主要是读入输入端信号，将其平方后写在输出端，重复length次后停止。

​         consumer模块：

​                          ![consumer](https://cloud.githubusercontent.com/assets/22683831/19847578/e533210c-9f82-11e6-8ab2-bc534fb00a31.png)

​        如上图所示：consumer_fire是信号消费函数，该函数通过比较当前位置与设定的长度，从而确定是读入输入端信号，并且打印；还是销毁进程，停下来。

​                         ![image](https://cloud.githubusercontent.com/assets/22683831/19853806/831932ee-9fa6-11e6-9cab-efc19a3443a8.png)

​        上图为进程的定义函数，在该函数中第一行的value值为迭代次数，变量名称为N；下面详细定义了该进程的变量名和端口号，如上述第一个process中，generation为模块的名字，output为未知数的类型，后面的10为，未知数的端口号。

​                       ![image](https://cloud.githubusercontent.com/assets/22683831/19853977/7807455c-9fa7-11e6-93fe-a631f4d1ea7a.png)

​         上图为通道的定义，一条线即为一条通道，上述定义了两个端口，一个为in，一个为out端口，fifo为缓冲区的名字，size为缓冲区的大小，C1为通道的名字。

​                    ![image](https://cloud.githubusercontent.com/assets/22683831/19854144/52d5503e-9fa8-11e6-874e-aa6dae0d1982.png)

​        上图为模块的连接过程，首先通过定义模块之间的连接，形成一条线，然后通过定义端口来连接这条线 ；在g-c这条线上，它从generation模块的1端口连接到c1这个模块的0端口，然后又从g-c线的其他端口连接到其他模块，从而实现模块之间的连接。

###### 3）代码修改如下

​                       ![image](https://cloud.githubusercontent.com/assets/22683831/19855403/56ada68c-9faf-11e6-8781-4184e3b438e5.png)

​        上图为代码修改图，在该试验中我们只需将value的值由3改为2，即将原来的三个模块变成两个模块即可。

###### 4）实验结果：



​                       ![image](https://cloud.githubusercontent.com/assets/22683831/19855183/2012356c-9fae-11e6-8510-35a5accb025e.png)

​     上述结果为修改后的结果截图，由于平方模块由三个变成了两个，所以数值由原来的8次方变为了现在的4次方。

#### 二.修改example1，使其输出三次方，tips：修改quare.c

###### 1)dol截图如下：

![dol](https://cloud.githubusercontent.com/assets/22683831/19846876/bf130f8c-9f7d-11e6-9d50-599f16adf6c4.jpg)

​        由于两个实验的模块和内容都一样，所以该模块内容不再具体分析，下面直接分析代码修改与实验截图。

###### 2）代码修改：

​              ![，](https://cloud.githubusercontent.com/assets/22683831/19855526/13f74c3e-9fb0-11e6-9954-b4296783cd88.png)

​        上述代码为实验修改代码，在由平方到立方的过程中，我们只需将平方函数中的i*i，修改为三次即可。

###### 3）结果截图：

​                             ![image](https://cloud.githubusercontent.com/assets/22683831/19855625/8c0443d0-9fb0-11e6-839c-cd58454ffe23.png)

​        实验结果如上图所示，该数据为0-19三次方后的结果。

#### 三.实验问题与解决办法

##### 实验问题：

1）在实验一的过程中，我一直在修改迭代的方法，意图将三个模块改为两个模块，不改变数的次方数

2）在实验二的过程中，修改了次方数，结果仍是没有改变

##### 解决方法：

1）在多次琢磨迭代函数的代码之后，有点心灰意冷，这时同学告诉我说：师兄说的只要修改迭代次数就好，我这才恍然大悟，知道了这次修改是要改变数据的，实验代码只是为了让我们了解过程而已。

2）在实验二的过程中，我尝试了多次，发现结果都是错误的，究其原因，这才发现原来我一直跑的文件都是经以前编译过的文件，这次虽然修改了代码，编译了文件，但是编译并没有改变文件的内容，所以最后我删掉了以前编译的文件，重新编译，得到了正确的结果。

#### 四.实验感想

这次实验虽然修改的代码不是很多，而且修改起来非常简单，但是这次实验的代码确实比较难以理解的，我们在这次的实验过程中要知道如何分析DOL文件,知道如何编程，如何得到dol图，而不是简单的完成实验内容。











