---
title: "kafaka基本使用"
date: "2023-04-26 18:12:00"
tags:
categories:
description: >-
  一、安装 创建docker-compose.yml version: "2" services: zookeeper: image: docker.io/bitnami/zookeeper:3.8 ports: - "2181:2181" volumes: - "zookeeper_data:/bi
---

# 一、安装
创建docker-compose.yml
```yml
version: "2"

services:
  zookeeper:
    image: docker.io/bitnami/zookeeper:3.8
    ports:
      - "2181:2181"
    volumes:
      - "zookeeper_data:/bitnami"
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes
  kafka:
    image: docker.io/bitnami/kafka:3.4
    ports:
      - "9092:9092"
      - "9093:9093"
    volumes:
      - "kafka_data:/bitnami"
    environment:
      - ALLOW_PLAINTEXT_LISTENER=yes
      - KAFKA_ENABLE_KRAFT=no
      - KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper:2181

      - KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CLIENT:PLAINTEXT,EXTERNAL:PLAINTEXT
      - KAFKA_CFG_LISTENERS=CLIENT://:9092,EXTERNAL://:9093
      - KAFKA_CFG_ADVERTISED_LISTENERS=CLIENT://kafka:9092,EXTERNAL://localhost:9093
      - KAFKA_CFG_INTER_BROKER_LISTENER_NAME=CLIENT
    depends_on:
      - zookeeper

volumes:
  zookeeper_data:
    driver: local
  kafka_data:
    driver: local
```

运行 docker compose up -d

# 二、使用
### 生产者代码
```golang
package main

import (
	"fmt"

	"github.com/Shopify/sarama"
)

func main() {

	// 一些配置
	config := sarama.NewConfig()
	config.Producer.RequiredAcks = sarama.WaitForAll          // 发送完数据需要leader和follow都确认
	config.Producer.Partitioner = sarama.NewRandomPartitioner // 新选出一个partition
	config.Producer.Return.Successes = true                   // 成功交付的消息将在success channel返回

	// 构造数据
	msg := &sarama.ProducerMessage{}
	msg.Topic = "web_log"
	msg.Key = sarama.StringEncoder("imkey")
	msg.Value = sarama.StringEncoder("imvalue")

	// 连接kafka
	client, err := sarama.NewSyncProducer([]string{"127.0.0.1:9093"}, config)
	if err != nil {
		fmt.Println("producer closed, err:", err)
		return
	}
	defer client.Close()

	// 发送消息
	pid, offset, err := client.SendMessage(msg)
	if err != nil {
		fmt.Println("send msg failed, err:", err)
		return
	}
	fmt.Printf("pid:%v offset:%v\n", pid, offset)
}
```

### 消费者代码
```golang
package main

import (
	"fmt"

	"github.com/Shopify/sarama"
)

func main() {

	// 连接consumer
	consumer, err := sarama.NewConsumer([]string{"127.0.0.1:9093"}, nil)
	if err != nil {
		fmt.Printf("fail to start consumer, err:%v\n", err)
		return
	}

	// 根据topic取到所有的分区
	partitionList, err := consumer.Partitions("web_log")
	if err != nil {
		fmt.Printf("fail to get list of partition:err%v\n", err)
		return
	}
	fmt.Println(partitionList)

	// 遍历所有的分区
	for partition := range partitionList {

		// 针对每个分区创建一个对应的分区消费者
		pc, err := consumer.ConsumePartition("web_log", int32(partition), sarama.OffsetNewest)
		if err != nil {
			fmt.Printf("failed to start consumer for partition %d,err:%v\n", partition, err)
			return
		}
		defer pc.AsyncClose()

		// 异步从每个分区消费信息
		go func(sarama.PartitionConsumer) {
			for msg := range pc.Messages() {
				fmt.Printf("Partition:%d Offset:%d Key:%v Value:%v", msg.Partition, msg.Offset, string(msg.Key), string(msg.Value))
			}
		}(pc)
	}

	select {}
}
```
