## Cartographer

#### 简介

​	**Cartographer**是Google开源的一个SLAM算法，基于激光雷达以及 IMU（惯性处理单元），我们要做的也就是将Cartographer安装在**ROS**中。

#### 安装流程（每一步的运行结果在后面给出截图）

1. 安装所有的**依赖项**

   ```
   sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/19538366.jpg)

2. 安装**ceres solver**

   ```
   git clone https://github.com/hitcm/ceres-solver-1.11.0.git
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/98331523.jpg)

   ```
   mkdir build
   cd ceres-solver-1.11.0/build
   ```

   ```
   cmake ..
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/59878948.jpg)

   ```
   make
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/33608823.jpg)

   ```
   sudo make install
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/36077971.jpg)

3. **安装 cartographer**

   ```
   git clone https://github.com/hitcm/cartographer.git
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/24375462.jpg)

   ```
   mkdir build
   cd cartographer/build
   ```

   ```
   cmake .. -G Ninja
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/66021113.jpg)

   ```
   ninja
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/11981600.jpg)

   ```
   ninja test
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/46077306.jpg)

   ```
   sudo ninja install
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/30744073.jpg)

4. **安装cartographer_ros**

   ```
   mkdir catkin_ws
   cd catkin_ws
   mkdir src
   cd src
   git clone https://github.com/hitcm/cartographer_ros.git
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/62463732.jpg)

   ```
   cd ..
   catkin_make
   ```

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/22654338.jpg)

   到这里所有的配置步骤已经完成了。

5. 进行数据**测试**

   首先我们需要下载**bag**文件，这里我是直接用迅雷下载的bag文件，然后拖到虚拟机中运行

   ```
   roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
   ```

   运行结果如下，大概经过了半个小时的生成，得到下图：

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-11-7/38106336.jpg)

   自此关于**Cartographer**的配置以及测试全部完成。

#### 实验感想

​	这次实验，我只想说，真的一波三折，其实开始的安装ceres solver以及cartographer还算正常，很顺利的就完成了。但是，在装cartographer_ros的时候就出问题了，先是照着TA给的方式配置了一下，这样还正常，可以得到结果。但是这里我clone的是TA的github，忘了改成官方的路径，然后在运行bag的时候就出问题了，调了半天才发现是这个问题。然后再次按照正确流程来，结果这次在catkin_make这里出错了。没办法，只能按照google给的官方文档配置，结果还是GG，但是这一步我另外安装了一个新的依赖项，然后再按照博客流程，就可以成功的catkin_make了。最终还是成功做出来了哈哈，当然也离不开TA的帮助。不过通过这反复的错误，也更深的了解到了Cartographer。