
---
layout: post
title: " 第四百一十六节，Tensorflow简介与安装 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


第四百一十六节，Tensorflow简介与安装

TensorFlow是什么

Tensorflow是一个Google开发的第二代机器学习系统，克服了第一代系统DistBelief仅能开发神经网络算法、难以配置、依赖Google内部硬件等局限性，应用更加广泛，并且提高了灵活性和可移植性，速度和扩展性也有了大幅提高。字面上理解，TensorFlow就是以张量（Tensor）在计算图（Graph）上流动（Flow）的方式的实现和执行机器学习算法的框架。具有以下特点：

  * 灵活性。TensorFlow不是一个严格的“神经网络”库。只要可以将计算表示成数据流图，就可以使用TensorFlow，比如科学计算中的偏微分求解等。（实际上其官网的介绍中对TF的定位就是基于数据流图的科学计算库，而非仅仅是机器学习库）
  * 可移植性。同一份代码几乎不经过修改既可以部署到有任意数量CPU、GPU或TPU（Tensor Processing Unit，Google专门为机器学习开发的处理器）的PC、服务器或移动设备上。
  * 自动求微分。同Theano一样，TensorFlow也支持自动求微分，用户不需要再通过反向传播求解梯度。
  * 多语言支持。TensorFlow官方支持Python、C++、Go和Java接口，用户可以在硬件配置较好的机器中用Python进行实验，在资源较紧张或需要低延迟的环境中用C++进行部署。
  * 性能。虽然TensorFlow最开始发布时仅支持单机，在性能评测上并不出色，但是凭借Google强大的开发实力，TensorFlow性能已经追上了其他框架

[code]

    Google第一代分布式机器学习框架DistBelief在内部大规模使用后没有选择开源，而第二代TensorFlow于2015年11月在GitHub上开源，并在持续快速开发迭代中。TensorFlow最早由Google Brain的工程师开发，设计初衷是加速机器学习的研究，并快速地将研究原型转化为产品。Google选择开源TensorFlow的原因很简单：第一是希望借助社区的力量，大家一起完善TensorFlow。第二是回馈社区，Google希望让这个优秀的工具得到更多的应用，提高学术界和工业界使用机器学习的效率。
[/code]

[code]

    自从2015年11月开源以来，TensorFlow迅速在众多的机器学习框架中脱颖而出，在Github上获得了最多的Star
[/code]

Google第一代分布式机器学习框架DistBelief在内部大规模使用后没有选择开源，而第二代TensorFlow于2015年11月在GitHub上开源，并在持续快速开发迭代中。TensorFlow最早由Google
Brain的工程师开发，设计初衷是加速机器学习的研究，并快速地将研究原型转化为产品。Google选择开源TensorFlow的原因很简单：第一是希望借助社区的力量，大家一起完善TensorFlow。第二是回馈社区，Google希望让这个优秀的工具得到更多的应用，提高学术界和工业界使用机器学习的效率。

自从2015年11月开源以来，TensorFlow迅速在众多的机器学习框架中脱颖而出，在Github上获得了最多的Star.



安装 pip install tensorflow

安装时会安装以下依赖

absl-py-0.4.1  
astor-0.7.1 gast-0.2.0  
grpcio-1.14.2  
markdown-2.6.11  
numpy-1.14.5  
protobuf-3.6.1  
setuptools-39.1.0  
six-1.11.0  
tensorboard-1.10.0  
termcolor-1.1.0  
werkzeug-0.14.1



**设置变量**

[code]

     import tensorflow as tf
    
    # python创建变量
    a = 3
    
    # tensorflow创建一个变量Variable
    # 创建横向量
    w = tf.Variable([[0.5, 1.0]])
    # 创建竖向量
    x = tf.Variable([[4.0], [1.0]])
    
    # 横向量乘以竖向量matmul
    y = tf.matmul(w, x)
    
    # 全局变量初始化global_variables_initializer
    init_op = tf.global_variables_initializer()
    with tf.Session() as sess:
        # 执行计算run
        sess.run(init_op)
        # 打印结果eval
[/code]

[code]

    [[ 2.]]
      
    注意：如果PyCharm提示以下信息，加两行代码即可  
    2018-09-10 21:02:19.937491: I T:\src\github\tensorflow\tensorflow\core\platform\cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2
[/code]

 import os  
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'  
#默认为0：输出所有log信息  
#设置为1：进一步屏蔽INFO信息  
#设置为2：进一步屏蔽WARNING信息

#设置为3：进一步屏蔽ERROR信息

[code]

    import tensorflow as tf
    import os
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
    
    # python创建变量
    a = 3
    
    # tensorflow创建一个变量Variable
    # 创建横向量
    w = tf.Variable([[0.5, 1.0]])
    # 创建竖向量
    x = tf.Variable([[4.0], [1.0]])
    
    # 横向量乘以竖向量matmul
    y = tf.matmul(w, x)
    
    # 全局变量初始化global_variables_initializer
    init_op = tf.global_variables_initializer()
    with tf.Session() as sess:
        # 执行计算run
        sess.run(init_op)
        # 打印结果eval
        print(y.eval())
[/code]



tensorflow很多操作跟numpy有些类似的

  * tf.zeros([3, 4], int32) ==> [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

  * tf.zeros_like(tensor) ==> [[0, 0, 0], [0, 0, 0]]

  * tf.ones([2, 3], int32) ==> [[1, 1, 1], [1, 1, 1]]

  * tf.ones_like(tensor) ==> [[1, 1, 1], [1, 1, 1]]

  * tensor = tf.constant([1, 2, 3, 4, 5, 6, 7]) => [1 2 3 4 5 6 7]

  * tensor = tf.constant(-1.0, shape=[2, 3]) => [[-1. -1. -1.] [-1. -1. -1.]]

  * tf.linspace(10.0, 12.0, 3, name="linspace") => [ 10.0 11.0 12.0]

  * tf.range(start, limit, delta) ==> [3, 6, 9, 12, 15]

** **

**随机**

[code]

     import tensorflow as tf
    import os
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
    
    # 生成的值服从具有指定平均值和标准偏差的正态分布
    norm = tf.random_normal([2, 3], mean=-1, stddev=4)
    
    # 洗牌
    c = tf.constant([[1, 2], [3, 4], [5, 6]])
    shuff = tf.random_shuffle(c)
    
    # 每一次执行结果都会不同
    sess = tf.Session()
    print(sess.run(norm))
    print(sess.run(shuff))
[/code]

[code]

    [[-5.58110332  0.84881377  7.51961231]
     [ 3.27404118 -7.22483826  7.70631599]]
    [[5 6]
     [1 2]
     [3 4]]
[/code]



**循环加1**



[code]

    import tensorflow as tf
    import os
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
    
    
    state = tf.Variable(0)
    
    # 每初始化一次加1
    # add加
    new_value = tf.add(state, tf.constant(1))
    # assign重新赋值
    update = tf.assign(state, new_value)
    
    with tf.Session() as sess:
        # 初始化
        sess.run(tf.global_variables_initializer())
        print(sess.run(state))
        # 循环3次
        for _ in range(3):
            sess.run(update)
            print(sess.run(state))
[/code]



[code]

    0
    1
    2
    3  
    
    
[/code]





**加减乘除**

[code]

     import tensorflow as tf
    import os
    
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
    
    a = tf.constant(5.0)
    b = tf.constant(10.0)
    
    ts1 = tf.constant(8.0)
    ts2 = tf.constant(9.0)
    
    x = tf.add(a, b, name="add")
    y = tf.div(a, b, name="divide")
    
    # （1）加法+
    ts_add1 = tf.add(ts1, ts2, name=None)
    ts_add2 = ts1 + ts2  # 二者等价
    # （2）减法-
    ts_sub1 = tf.subtract(ts1, ts2, name=None)
    ts_sub2 = ts1 - ts2  # 二者等价
    # （3）乘法*
    ts_mul1 = tf.multiply(ts1, ts2, name=None)
    ts_mul2 = ts1 * ts2
    # （4）除法/
    ts_div1 = tf.divide(ts1, ts2, name=None)
    ts_div2 = tf.div(ts1, ts2, name=None)  # div 支持 broadcasting(即shape可不同)
    ts_div3 = ts1 / ts2
    
    
    with tf.Session() as sess:
        print("a =", sess.run(a))
        print("b =", sess.run(b))
        print("a + b =", sess.run(x))
        print("a/b =", sess.run(y))
        print("ts_sub1", sess.run(ts_sub1))
[/code]

a = 5.0  
b = 10.0  
a + b = 15.0  
a/b = 0.5  
ts_sub1 -1.0



**挖坑**



[code]

    import tensorflow as tf
    import os
    
    os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'
    
    # 理解为挖一个32的坑
    input1 = tf.placeholder(tf.float32)
    input2 = tf.placeholder(tf.float32)
    
    # 两个坑相乘
    output = tf.multiply(input1, input2)
    
    with tf.Session() as sess:
        # 分别向两个坑填数据feed_dict
        print(sess.run([output], feed_dict={input1: [7.], input2: [2.]}))
[/code]



[code]

    [array([ 14.], dtype=float32)]
[/code]





[叫卖录音网](http://www.jxiou.com/)  
[录音网站](http://www.jxiou.com/lu_yin_wang_zhan.html)

