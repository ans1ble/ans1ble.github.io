
---
layout: post
title: " 第二百九十二节，RabbitMQ多设备消息队列-Python开发 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**RabbitMQ多设备消息队列-Python开发**

**首先安装 **Python开发连接 **RabbitMQ的API，pika模块******

************pika模块为第三方模块************



************  对于RabbitMQ来说，生产和消费不再针对内存里的一个Queue对象，而是某台服务器上的RabbitMQ
Server实现的消息队列。************



* * *



**生产者消费者一对一**

**不使用交换机**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170622144408804-1561852360.png)



**生产者主机**

**pika.PlainCredentials() 设置RabbitMQ Server用户名和密码**  
 **ConnectionParameters() 设置ip和端口**  
 **BlockingConnection() 创建连接，自带了socket逻辑部分**  
 **channel() 获取连接句柄**  
 **queue_declare(queue='队列名称') 向RabbitMQ Server创建一个消息队列，如果此队列存在则不创建**  
 **basic_publish(exchange='交换机状态',routing_key='队列名称',body='数据类容') 向指定队列里写入数据**  
 **close() 关闭连接**

[code]

    #!/usr/bin/env python
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 生产者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.queue_declare(queue='hello')                    #向RabbitMQ Server创建一个消息队列，queue='hello'设置队列名称，如果此队列存在则不创建
    
    #向指定队列里写入数据
    channel.basic_publish(exchange='',                      #exchange路由交换机，参数为空，路由交换机不工作
                          routing_key='hello',              #routing_key设置数据放到指定名称的消息队列里，参数是队列名称
                          body='123')                       #body设置数据内容，参数是要写入指定队列的数据
    
    connection.close()                                                  #关闭连接
[/code]

**生产者执行了7次，可以看到hello队列里有7条数据**

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170622165931429-1151443746.png)



**消费者主机**

**callback(ch, method, properties, (body接收队列里的数据))** **自定义获取队列数据后的回调函数**

**basic_consume(回调函数名称,queue='队列名称',no_ack=True)
在指定队列里获取数据，no_ack=True设置获取到数据后，是否删除队列里对应的数据**  
 **start_consuming() 等待获取队列数据**

[code]

    #!/usr/bin/env python
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.queue_declare(queue='hello')                    #向RabbitMQ Server创建一个消息队列，queue='hello'设置队列名称，如果此队列存在则不创建
    
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print(" 你好 %r" % body)
    
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue='hello',                    #指定获取数据的队列名称
                          no_ack=True)                     #设置获取到数据后，是否删除队列里对应的数据，如果回调函数处理数据异常时会都丢失数据
                                                            #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    
    channel.start_consuming()                               #等待获取队列数据
[/code]

**执行后循环获取了7次，将hello队列里的7条数据拿了出来**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170622170507851-1393266366.png)**

**可以看到 **hello队列里已经没有了数据****

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170622172152632-2126900208.png)**





* * *





**保证数据不丢失介绍**

**保证消费者数据不丢失**

**当消费者主机从队列里拿出数据时basic_consume()方法参数no_ack=True，表示拿出数据后立即删除队列里对应的数据，**

**如果消费者主机拿出数据，队列也删除了对应的数据，还没来得及处理数据，消费者主机死机了，这样数据就丢了**

**解决方法：**

****当消费者主机从队列里拿出数据时 basic_consume()方法参数no_ack=False，表示
**拿出数据后不删除队列里对应的数据******

******在消费者回调函数里处理数据，当数据处理完成后写上 ch.basic_ack(delivery_tag =
method.delivery_tag)，表示执行这串代码后才删除队列里对应的数据******

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.queue_declare(queue='helloa',durable=True)         #向RabbitMQ Server创建一个消息队列，queue='hello'设置队列名称，如果此队列存在则不创建
    
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print(" 你好 %r" % body)
        ch.basic_ack(delivery_tag=method.delivery_tag)      #执行这串代码后才删除队列里对应的数据
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue='helloa',                    #指定获取数据的队列名称
                          no_ack=False)                     #设置获取到数据后，是否删除队列里对应的数据，如果回调函数处理数据异常时会都丢失数据
                                                            #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    
    channel.start_consuming()                               #等待获取队列数据
[/code]



****保证生产者数据不丢失****

**如果RabbitMQ Server主机队列里有很多数据，此时RabbitMQ Server主机死机了，那么队列里的数据也就丢了**

**解决方法：**

**当生产者向RabbitMQ Server主机队列投递数据时，数据同时也在RabbitMQ Server主机硬盘保存一份，那么即使死机重启后数据也存在**

**basic_publish(properties=pika.BasicProperties(delivery_mode=2))
投递模式默认为1，修改成2表示投递的数据在RabbitMQ Server主机硬盘上保存一份，当消费者操作后删除队列数据时，也跟随删除**  
 **queue_declare(durable=True) 表示队列里的数据开启硬盘保存，注意：如果生产者设置了那么消费者也要设置**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 生产者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.queue_declare(queue='helloa',durable=True)       #durable=True,表示队列里的数据开启硬盘保存
    
    #向指定队列里写入数据
    channel.basic_publish(exchange='',                      #exchange路由交换机，参数为空，路由交换机不工作
                          routing_key='helloa',              #routing_key设置数据放到指定名称的消息队列里，参数是队列名称
                          body='123',                       #body设置数据内容，参数是要写入指定队列的数据
                          properties=pika.BasicProperties(delivery_mode=2))   # 投递模式默认为1，修改成2表示投递的数据在RabbitMQ Server主机硬盘上保存一份，当消费者操作后删除队列数据时，也跟随删除
    
    
    connection.close()                                                  #关闭连接
[/code]



* * *





**消息获取顺序**

**默认消息队列里的数据是按照顺序被消费者拿走，例如：消费者1 去队列中获取 奇数 序列的任务，消费者2去队列中获取 偶数 序列的任务。**

**谁来谁取，不再按照奇偶数排列**

**在消费者获取队列数据方法
basic_consume()之前写一个channel.basic_qos(prefetch_count=1)表示谁来谁取，不再按照奇偶数排列**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.queue_declare(queue='helloa',durable=True)         #向RabbitMQ Server创建一个消息队列，queue='hello'设置队列名称，如果此队列存在则不创建
    
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print(" 你好 %r" % body)
        ch.basic_ack(delivery_tag=method.delivery_tag)      #执行这串代码后才删除队列里对应的数据
    
    channel.basic_qos(prefetch_count=1)                     #表示谁来谁取，不再按照奇偶数排列
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue='helloa',                    #指定获取数据的队列名称
                          no_ack=False)                     #设置获取到数据后，是否删除队列里对应的数据，如果回调函数处理数据异常时会都丢失数据
                                                            #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    
    channel.start_consuming()                               #等待获取队列数据
[/code]



* * *





#### exchange交换机工作模型（fanout发布订阅，direct关键字发送，topic模糊匹配）

#### **fanout交换机，发布订阅模式**

**发布者发布数据到交换机，交换机将数据分发到所有订阅者创建的队列里， 每个订阅者主机都获取一份数据**

**列队只能由订阅者创建，订阅者创建的列队只要绑定了交换机都会获取到，交换机分发的数据**

**发布订阅和简单的消息队列区别在于，发布订阅会将消息发送给所有的订阅者，而消息队列中的数据被消费一次便消失。所以，RabbitMQ实现发布和订阅时，会为每一个订阅者创建一个队列，而发布者发布消息时，交换机会将消息放置在所有相关队列中。**

**exchange type = fanout**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170623045136366-797009509.png)**

**  发布者**

[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    import sys
    
    # ######################### 发布者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='fanout'交互机工作模式fanout为订阅模式
                             type='fanout')
    
    message = ' '.join(sys.argv[1:]) or "info: Hello World!"    #设置向交换机发布的数据内容
    
    #向交换机发布内容
    channel.basic_publish(exchange='logs',     #设置要发布的交换机名称
                          routing_key='',      #队列名称为空，因为数据是发布到交换机而不是队列，所以为空
                          body=message)        #设置要发布的数据内容
    print("数据内容以发布到交换机")
    
    connection.close()                                                 #关闭连接
[/code]

**订阅者**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 订阅者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='fanout'交互机工作模式fanout为订阅模式
                             type='fanout')
    
    result = channel.queue_declare(exclusive=True)          #创建专一订阅消息队列，
    queue_name = result.method.queue                        #随机生成队列名称
    
    #将订阅队列绑定交换机
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name)                    #queue=要绑定交换机的队列名称
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print("%r" % body)
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue=queue_name,                 #指定获取数据的队列名称
                          no_ack=True)                      #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    channel.start_consuming()                               #等待获取队列数据
    
[/code]

* * *
[code]

    #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 订阅者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='fanout'交互机工作模式fanout为订阅模式
                             type='fanout')
    
    result = channel.queue_declare(exclusive=True)          #创建专一订阅消息队列，
    queue_name = result.method.queue                        #随机生成队列名称
    
    #将订阅队列绑定交换机
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name)                    #queue=要绑定交换机的队列名称
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print("%r" % body)
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue=queue_name,                 #指定获取数据的队列名称
                          no_ack=True)                      #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    channel.start_consuming()                               #等待获取队列数据
[/code]



* * *



####  

#### **direct交换机，关键字发送模式**

**exchange type = direct**

**也叫做完全匹配模式**

**RabbitMQ还支持根据关键字发送，即：队列绑定关键字，生产者设置关键字将数据发送到exchange交换机，exchange交换机根据
消费者列队设置的关键字 判定应该将数据发送至指定队列。**

**也就是说消费者列队设置的关键字，和生产者发送数据设置的关键字 ，两者只要是一样关键字的，消费者主机都会获取到一份数据**

**【重点】 消费者可以设置多个关键字**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170623175754023-1060633775.png)**



**生产者**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    import sys
    
    # ######################### 生产者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='direct'交互机工作模式direct为关键字发送模式
                             type='direct')
    
    message = ' '.join(sys.argv[1:]) or "info: Hello World!"    #设置向交换机发布的数据内容
    
    #向交换机发布内容
    channel.basic_publish(exchange='logs',          #设置要发布的交换机名称
                          routing_key='severity',   #设置信道关键字
                          body=message)             #设置要发布的数据内容
    print("数据内容以发布到交换机")
    
    connection.close()                                                 #关闭连接
[/code]

**消费者，设置一个信道关键字**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='direct'交互机工作模式direct为关键字发送模式
                             type='direct')
    
    result = channel.queue_declare(exclusive=True)          #创建专一消息队列，
    queue_name = result.method.queue                        #随机生成队列名称
    
    #将队列绑定交换机
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name,                    #queue=要绑定交换机的队列名称
                       routing_key='severity',)             #设置信道关键字
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print("%r" % body)
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue=queue_name,                 #指定获取数据的队列名称
                          no_ack=True)                      #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    channel.start_consuming()                               #等待获取队列数据
[/code]

**消费者，设置多个信道关键字**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='direct'交互机工作模式direct为关键字发送模式
                             type='direct')
    
    result = channel.queue_declare(exclusive=True)          #创建专一消息队列，
    queue_name = result.method.queue                        #随机生成队列名称
    
    #将队列绑定交换机
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name,                    #queue=要绑定交换机的队列名称
                       routing_key='severity',)             #设置信道关键字
    
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name,                    #queue=要绑定交换机的队列名称
                       routing_key='severity2',)             #设置信道关键字
    
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name,                    #queue=要绑定交换机的队列名称
                       routing_key='severity3',)             #设置信道关键字
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print("%r" % body)
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue=queue_name,                 #指定获取数据的队列名称
                          no_ack=True)                      #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    channel.start_consuming()                               #等待获取队列数据
[/code]



* * *





#### ****  topic**交换机，模糊匹配发送模式**

**exchange type = topic**

**在topic类型下，可以让队列绑定几个模糊的关键字，之后发送者将数据发送到exchange交换机，exchange交换机将传入的”列队关键字“和
”生产者关键字“进行匹配，匹配成功，则将数据发送到指定队列。**

  * **# 表示可以匹配 0 个 或 多个 单词**
  * ***  表示只能匹配 一个 单词**

**例如：**

[code]

     发送者关键字               生产者匹配
    old.boy.python          old.*  -- 不匹配
    old.boy.python          old.#  -- 匹配
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170623185315195-485322930.png)



**生产者**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    import sys
    
    # ######################### 生产者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='topic'交互机工作模式topic为模糊匹配发送模式
                             type='topic')
    
    routing_key = sys.argv[1] if len(sys.argv) > 1 else 'anonymous.info'  #设置发送关键字
    message = ' '.join(sys.argv[2:]) or 'Hello World!'                    #设置发送内容
    
    #向交换机发送内容
    channel.basic_publish(exchange='logs',              #设置要发布的交换机名称
                          routing_key=routing_key,      #设置信道关键字：anonymous.info
                          body=message)                 #设置要发布的数据内容：Hello World!
    
    print(" [x] Sent %r:%r" % (routing_key, message))   #打印出相关内容
    
    connection.close()          #关闭连接
[/code]

**消费者**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    
    import pika  #导入连接操作RabbitMQ Server主机的模块
    
    # ######################### 消费者 #########################
    
    credentials = pika.PlainCredentials('guest', 'guest')                      #设置RabbitMQ Server用户名和密码
    parameters = pika.ConnectionParameters('localhost', 5672,'/',credentials)  #设置ip和端口
    
    connection = pika.BlockingConnection(parameters)        #创建连接，自带了socket逻辑部分
    channel = connection.channel()                          #获取连接句柄
    
    
    channel.exchange_declare(exchange='logs',               #创建交换机，exchange='交换机名称'，type='topic'交互机工作模式topic为模糊匹配发送模式
                             type='topic')
    
    result = channel.queue_declare(exclusive=True)          #创建专一消息队列，
    queue_name = result.method.queue                        #随机生成队列名称
    
    #将队列绑定交换机
    channel.queue_bind(exchange='logs',                     #exchange='要绑定的交换机名称'
                       queue=queue_name,                    #queue=要绑定交换机的队列名称
                       routing_key='anonymous.*',)             #设置信道关键字匹配
    
    def callback(ch, method, properties, body):             #定义获取队列数据后的回调函数，body接收队列里的数据内容
        print("%r" % body)
    
    #在指定队列里获取数据
    channel.basic_consume(callback,                         #获取到数据后执行回调函数
                          queue=queue_name,                 #指定获取数据的队列名称
                          no_ack=True)                      #如果要保证数据必须不丢失设置为False不删除数据,当接执行回调函数里ch.basic_ack(delivery_tag=method.delivery_tag)时才删除，但是效率不高
    
    channel.start_consuming()                               #等待获取队列数据
[/code]



**更多教程，可以查看官方教程**

**http://www.rabbitmq.com/getstarted.html**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170623201235991-2064759703.png)**



