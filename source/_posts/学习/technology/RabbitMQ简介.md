---
title: RabbitMQ简介
date: 2021-08-011 09:12:04
author: 乔亚峰
top: true
toc: true
mathjax: false
summary: RabbitMQ is the most widely deployed open source message broker.
categories: RabbitMQ
tags:
  - RabbitMQ
  - 博客
---


RabbitMQ is the most widely deployed open source message broker.

RabbitMQ is lightweight and easy to deploy on premises and in the cloud. It supports multiple messaging protocols. RabbitMQ can be deployed in distributed and federated configurations to meet high-scale, high-availability requirements.

RabbitMQ是一个消息代理。它的工作就是接收和转发消息。你可以把它想像成一个邮局：你把信件放入邮箱，邮递员就会把信件投递到你的收件人处。在这个比喻中，RabbitMQ就扮演着邮箱、邮局以及邮递员的角色。

RabbitMQ和邮局的主要区别在于，它处理纸张，而是接收、存储和发送消息（message）这种二进制数据。

下面是RabbitMQ和消息所涉及到的一些术语。

- 生产(Producing)的意思就是发送。发送消息的程序就是一个生产者(producer)。我们一般用"P"来表示:

[producer](img/producer.png)

- 队列(queue)就是存在于RabbitMQ中邮箱的名称。虽然消息的传输经过了RabbitMQ和你的应用程序，但是它只能被存储于队列当中。实质上队列就是个巨大的消息缓冲区，它的大小只受主机内存和硬盘限制。多个生产者（producers）可以把消息发送给同一个队列，同样，多个消费者（consumers）也能够从同一个队列（queue）中获取数据。队列可以绘制成这样（图上是队列的名称）：
[queue](img/queue.png)

- 在这里，消费（Consuming）和接收(receiving)是同一个意思。一个消费者（consumer）就是一个等待获取消息的程序。我们把它绘制为"C"：
[producer](img/producer.png)

需要指出的是生产者、消费者、代理需不要待在同一个设备上；事实上大多数应用也确实不在会将他们放在一台机器上。



[python-one](img/python-one.png)

[RabbitMQ官网](https://www.rabbitmq.com/)
[文章参考](https://www.rabbitmq.com/tutorials/tutorial-one-python.html)