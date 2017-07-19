# rabbitmq

## 综述

rabbitmq是一个消息队列服务. 执行一些耗时的任务, 以减缓对API服务的压力.

## 部署流程

```
docker pull rabbitmq:3.6.10-management

docker run -d -p 15672:15672 -p 4379:4379 -e RABBITMQ_DEFAULT_USER=glrh11 -e RABBITMQ_DEFAULT_PASS=rabbitmq -v /home/glrh11/workspace/rabbitmqdata:/var/lib/rabbitmq --hostname my-rabbit --name rabbitmq rabbitmq:3.6.10-management
```

管理后台地址: http://*****:15672/#/
管理后台登录账号 ***:rabbitmq
