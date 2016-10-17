## DOL实例分析&编程

#### 实验结果截图

* example1 dot截图

![](http://p1.bpimg.com/567571/76a734c41ae8554e.png)

* example2 dot截图

![](http://p1.bpimg.com/567571/b25a8efbc1ca4922.png)

#### 实验过程解释

* example1

  这里我们的实验目的是修改example1，使其输出3次方数，所以可以知道这里需要修改的是运算过程，直接去到square.c中修改即可，先看原始未修改的情况

  ```c
  if (p->local->index < p->local->len) {
          DOL_read((void*)PORT_IN, &i, sizeof(float), p);
          i = i*i;
          DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
          p->local->index++;
      }
  ```

  可以看到这里的`i*i`即代表平方，我们只需要将其修改成三次方即可

  ```c
  if (p->local->index < p->local->len) {
          DOL_read((void*)PORT_IN, &i, sizeof(float), p);
          i = i*i*i;
          DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
          p->local->index++;
      }
  ```

  以上就是example1的修改过程，这里的过程就直接到对应的c文件中修改就OK了

* example2

  这里我们的实验目的是修改example2，让 3个square模块变成 2个，可知这里与三个c文件都没关系，我们需要修改的就是运算逻辑过程，需要将平方模块的迭代次数从3次变成2次，在xml文件中查看相关代码

  ```xml
  <variable value="2" name="N"/>
  ```

  可以看到开始有定义一个变量值，这里我把修改成了2

  ```xml
  <iterator variable="i" range="N">
      <process name="square">
        <append function="i"/>
        <port type="input" name="0"/>
        <port type="output" name="1"/>
        <source type="c" location="square.c"/>
      </process>
    </iterator>
  ```

  在xml文件中定义了这个迭代器，我们这里将其设置成2，即可达成只实现两次的迭代的目的，最终结果就和上面的一样，模块减少成了2个。

#### 实验感想

​	这次实验过程相对来说比较容易，需要修改的地方也不多，单是学到的东西还是挺多的，首先是了解到了在example文件夹中每个文件的类型以及它们的作用，然后就是对每一个c代码以及xml代码进行理解，理解了dot文件的生成条件，需要怎样去定义这些进程以及通道，第二个实验就提到了一点迭代的知识，可以通过迭代定义多个相同模块，也可以生成连接connection。最后也希望之后的实验也能顺利去完成！