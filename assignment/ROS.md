## ROS安装

#### ROS

​	Robot operation system，一套框架，底层提供硬件驱动，软件层 面支持通用的文件格式。我们需要在Ubuntu中安装ROS

#### 安装过程

1. 安装sources.list

   ```java
   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
   ```

   用中大的链接也可以：

   ```java
   sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
   ```

2. 安装Keys

   ```java
   sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
   ```

3. 安装ros

   ``` java
   sudo apt-get update
   ```

   这里我们需要进行的是Desktop-Full install

   ```
   sudo apt-get install ros-jade-desktop-full
   ```

   ```
   apt-cache search ros-jade
   ```

4. 初始化rosdep

   在使用ROS之前，必须对其进行初始化的操作

   ```
   sudo rosdep init
   ```

   ```
   rosdep update
   ```

5. 环境的安装

   ```
   echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
   ```

   ```
   source ~/.bashrc
   ```

   如果想改变当前的shell，可以输入以下命令

   ```
   source /opt/ros/jade/setup.bash
   ```

6. 得到rosinstall

   rosinstall是一个工具，可以帮助下载很多ROS的资源

   ```
   sudo apt-get install python-rosinstall
   ```

自此ROS的安装过程已经over，可以检查一下，这里使用TA给的方法检查ROS系统

```
roswtf
```

![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/23296496.jpg)

#### 实验感想

这次实验过程和第一次实验一样，也是配置一个实验环境，不过配置一个环境首先就要了解它的用处，我理解的ROS像是一个系统，它是一套系统框架，然后它上面可以运行很多算法，就像PPT上讲的SLAM算法，这些算法以及对应的数据集就可以在ROS上实现，这些也是了解到了一个新事物。