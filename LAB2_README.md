## DOL开发环境配置

### DOL框架描述：

> **The distributed operation layer (DOL) is a software development framework to program parallel applications. **

##### 

##### DOL的概述包含以下三个方面：

* **DOL Application Programming Interface:** The DOL defines a set of computation and communication routines that enable the programming of distributed, parallel applications for the SHAPES platform. Using these routines, application programmers can write programs without having detailed knowledge about the underlying architecture. In fact, these routines are subject to further refinement in the hardware dependent software (HdS) layer.

* **DOL Functional Simulation:** To provide programmers a possibility to test their applications, a functional simulation framework has been developed. Besides functional verification of applications, this framework is used to obtain performance parameters at the application level.

* **DOL Mapping Optimization:** The goal of the DOL mapping optimization is to compute a set of optimal mappings of an application onto the SHAPES architecture platform. In a first step, XML based specification formats have been defined that allow to describe the application and the architecture at an abstract level. Still, all the information necessary to obtain accurate performance estimates is contained.

  ​

  ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/76289608.jpg)

  ​

### DOL安装过程

#### **在安装之前需要先了解Ant的优点**：

* **跨平台性**。Ant是纯java语言编写的，所示具有很好的跨平台性。
* **操作简单**。Ant是由一个内置任务和可选任务组成的。
* 容易**维护和书写**，结构清晰。
* Ant可以集成到**开发环境**中。

#### **接下来就开始介绍安装过程（代码后给出完成时的截图）**：

1. ##### 安装一些**必要的环境**

   `sudo apt-get update`

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/4466977.jpg)

   ##### `sudo apt-get install ant`

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/66220134.jpg)

   `sudo apt-get install openjdk-7-jdk`

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/3769444.jpg)

   `sudo apt-get install unzip`

   ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/76132933.jpg)

   ​

2. ##### **下载文件**

   这里我们需要两个压缩包分别为[systemc-2.3.1.tgz](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz)和[dol_ethz.zip](http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip),当然可以直接从自己的主机中拷贝到虚拟机中，另外也可以直接在网上下载

   ```perl
   sudo wget http://www.accellera.org/images/downloads/standards
   /systemc/systemc-2.3.1.tgz
   sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
   ```

   ​

3. ##### **解压文件**

   * 建立一个**dol**的文件夹

     `mkdir dol`

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/39037807.jpg)

   ​	可以看到我们的目录里面出现了这个**dol**目录，我这里在根目录建立

   * 将刚才下载的**dol_ethz**解压到**dol**这个文件夹中

     `unzip dol_ethz.zip -d dol`

   * 解压下载的**systemc-2.3.1.tgz**，同样解压到根目录下

     `tar -zxvf systemc-2.3.1.tgz`

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/85187307.jpg)

   ​

4. ##### **编译systemc**

   * 进入到刚才解压的**systemc-2.3.1**中

     `cd systemc-2.3.1`

   * 新建一个临时文件夹**objdir**

     `mkdir objdir`

   * 进入该文件夹**objdir**

     `cd objdir`

   * 在命令行里面运行**configure**，这个是根据系统的环境设置一下参数

     `../configure CXX=g++ --disable-async-updates`

     可以得到下面的结果：

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/19080180.jpg)

   * 开始**编译**

     `sudo make install`

     编译之后，可以得到下图所示结果：

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/84955191.jpg)

     `cd ..`

     `ls`

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/39901971.jpg)

     我们打开编译完的目录如上面所示，然后我们记下我们的**工作路径**

     `pwd`

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/1001131.jpg)

     这个路径在之后的配置中会起到作用

   ​

5. ##### **编译DOL**

   * ##### 进入刚刚新建的**dol**文件夹中

     `cd ../dol`

   * 修改dol里面的**build_zip.xml**文件

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/82231026.jpg)

     用**gedit**打开这个文件

     ```
     <property name="systemc.inc" value="YYY/include"/>
     <property name="systemc.lib" value="YYY/lib-linux
     /libsystemc.a"/>
     ```

     将上面两句代码里面的**YYY**改成之前**pwd**的结果，也就是上面得到的

     `/home/magic/systemc-2.3.1`

   * 进行**编译**

     `ant -f build_zip.xml all`

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/96914218.jpg)

     这个步骤完成之后显示上图结果，即**BUILD SUCCESSFUL**

   * 运行**例子**进行验证

     `cd build/bin/main`

     `ant -f runexample.xml -Dnumber=1`

     运行上面两行命令，得到以下结果：

     ![](http://7xrn7f.com1.z0.glb.clouddn.com/16-9-29/13423776.jpg)

     可以发现**BUILD SUCCESSFUL**。至此，DOL开发环境**配置完成**

### 实验感想

​	**本次实验内容是DOL开发环境配置，总的来说按照步骤来并不难，但重要的是要去理解DOL框架。但配置过程可谓坎坷，重装了三遍才完成，中间有些小错误没发现，到最后就只能重来，所以也给了自己一点教训，望以后能够细心一点，当然装好了皆大欢喜，希望之后的实验都能顺利完成！**