# Avatar

阿凡达，寓意信息的链接

Avatar 是 36node 团队采用的消息总线方案，用于日志采集和微服务间的异步通知。

## 访问方式

https://kibana.{domain}

## 查看状态

```
helm status elasticsearch -n { namespace }
helm status kafka -n { namespace }
helm status vector -n { namespace }
```

## 用 kafkacat 进行测试

```
kubectl run kafka-client --restart='Never' --image confluentinc/cp-kafkacat --command -- sleep infinity
kubectl exec --tty -i kafka-client -- bash

kafkacat -b kafka.data:9092 -C -t tbox -o end

```

## 清理索引的方法

https://www.ibm.com/docs/en/cloud-private/3.2.0?topic=configuration-manually-removing-log-indices
