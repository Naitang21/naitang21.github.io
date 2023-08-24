---
layout: post
title: template page
categories: [cate1, cate2]
description: some word here
keywords: keyword1, keyword2
typora-root-url: ..
mermaid: false
sequence: false
flow: false
mathjax: false
mindmap: false
mindmap2: false
---

## RabbitMQ基本概念

![image-20230812172334322](/images/posts/RabbitMQ/image-20230812172334322.png)

![image-20230812172451069](/images/posts/RabbitMQ/image-20230812172451069.png)



## RabbitMQ安装与启动

### Erlang安装

因为RabbitMQ是使用Erlang开发的，所以安装RabbitMQ的前提需要安装Erlang

下载地址：[Erlang Programming Language](https://link.zhihu.com/?target=https%3A//www.erlang.org/downloads)

下载后一路next即可

注意：还要新增系统变量：**ERLANG_HOME**，填写安装地址

在path中增加`%ERLANG_HOME%\bin`

在CMD命令行中输入 **erl**有版本号出现，即安装成功

### RabbitMQ安装

下载地址：[Downloading and Installing RabbitMQ — RabbitMQ](https://link.zhihu.com/?target=https%3A//www.rabbitmq.com/download.html)

![img](/images/posts/RabbitMQ/v2-b6baacce8c1080a6359c23e374f28fdd_1440w.webp)

![img](/images/posts/RabbitMQ/v2-204841e2c498527dc33aad956cbd82eb_r.jpg)

下载之后进行安装，安装完之后会自动启动服务，打开http://localhost:15672/会进入Rabbitmq登录页面，初始账户和密码都是guest

![image-20230812235319288](/images/posts/RabbitMQ/image-20230812235319288.png)



### RabbitMQ安装后无法启动--C盘User中文名问题导致

打开RabbitMQ安装目录中的sbin目录，进入cmd `set RABBITMQ_BASE=安装路径\data`

然后`rabbitmq-plugins enable rabbitmq_management`

重新进入登录页面即可



## RabbitMQ消费消息的模式

![image-20230812222208968](/images/posts/RabbitMQ/image-20230812222208968.png)

## Spring boot整合RabbitMQ

1. 添加Maven或Gradle依赖：在您的`pom.xml`（或`build.gradle`）文件中添加RabbitMQ的依赖项

   1. Maven

   ```
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-amqp</artifactId>
   </dependency>
   ```

   2. Gradle

   ```
   implementation 'org.springframework.boot:spring-boot-starter-amqp'
   ```

   

2. 配置RabbitMQ连接：在`application.properties`文件中添加以下配置：

```
spring.rabbitmq.host=your_rabbitmq_host
spring.rabbitmq.port=your_rabbitmq_port
spring.rabbitmq.username=your_rabbitmq_username
spring.rabbitmq.password=your_rabbitmq_password
```

3. 配置队列：

```java
import org.springframework.amqp.core.Queue;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class RabbitMQConfig {

    @Bean
    public Queue queue() {
        return new Queue("your_queue_name");
    }
}
```

4. 创建生产者：编写一个发送消息的生产者类，发送消息到RabbitMQ的指定队列中。您可以使用`RabbitTemplate`来发送消息。

```
import org.springframework.amqp.core.Queue;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MessageProducer {

    private final RabbitTemplate rabbitTemplate;
    private final Queue queue;

    @Autowired
    public MessageProducer(RabbitTemplate rabbitTemplate, Queue queue) {
        this.rabbitTemplate = rabbitTemplate;
        this.queue = queue;
    }

    public void send(String message) {
        rabbitTemplate.convertAndSend(queue.getName(), message);
        System.out.println("Message sent: " + message);
    }
}
```

5. 创建消费者：编写一个消费者类，用于从指定队列接收消息并处理它们。可以使用`@RabbitListener`注解来标记消费者方法，并使用`@QueueBinding`注解将队列绑定到该方法。

```java
import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.stereotype.Component;

@Component
public class MessageConsumer {

    @RabbitListener(queues = "your_queue_name")
    public void receive(String message) {
        System.out.println("Message received: " + message);
        // 进行消息处理逻辑
    }
}
```


6. 启动应用程序：

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class RabbitMQApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(RabbitMQApplication.class, args);

        // 获取消息生产者 bean
        MessageProducer producer = context.getBean(MessageProducer.class);

        // 发送消息
        producer.send("Hello, RabbitMQ!");
    }
}
```

启用RabbitMQ支持：在您的Spring Boot应用程序主类上添加`@EnableRabbit`注解以启用RabbitMQ支持。