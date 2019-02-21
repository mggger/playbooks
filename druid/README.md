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
**需指定host和配置文件夹**
1. 启动master 
```shell
ansible-playbook --skip-tags sdata,squery add_server.yml -e "host=druid_master conf_dir=/Users/home/git/playbooks/druid/conf" -u root
```    

2. 启动data server
```shell
ansible-playbook --skip-tags smaster,squery add_server.yml -e "host=druid_d_01 conf_dir=/Users/home/git/playbooks/druid/conf" -u root
```

3. 启动query server
```shell
ansible-playbook --skip-tags smaster,sdata add_server.yml -e "host=druid_q_01 conf_dir=/Users/home/git/playbooks/druid/conf" -u root
```


#### 检测服务是否启动成功
ansible zoo -m shell -a "jps" -u root