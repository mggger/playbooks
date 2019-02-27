# Druid 高可用集群安装 
使用的是[imply](https://static.imply.io/release/imply-2.8.14.tar.gz)集成包

## 相应的服务
1.  master server 高可用可部署2个master， 避免单点故障
    - coordinator     8081
    - overload node   8090
    
2.  data server  随着数据聚合的任务数递增 可以通过增加data server来解决
    - Druid Middle Manager 8091
    - Druid Historical     8083
    
3.  query server 随着query请求数递增， 可以通过增加queyr server来解决
    - Broker 8082
    - Imply UI 9095

### How to run 
1. Install service
```shell
 ansible-playbook install_service.yml -e "host=xxxxx" -u root
```

2. Start service 需要指定host和conf_dir
tags对应的服务为:
    - cc copy conf
    - sm start master
    - sd start data server
    - sq start query server

示例： 复制配置， 启动data server
```shell
 ansible-playbook --tags=cc, sd start_service.yml -e "host=druid_d_01 conf_dir=/Users/home/git/ansible-playbook/conf" -u root
```
