# 安装zookeeper集群

## 新机器
1. 安装java并且指定环境变量
2. 下载[zookeeper](http://apache.mirrors.ionfish.org/zookeeper/zookeeper-3.4.13/zookeeper-3.4.13.tar.gz)
3. 解压， 解压路径为/opt/bigdata/zookeeper
4. 进入zookeeper创建data目录， 并且生成特定的server_id 


## 所有的机器
1. 下发相同的配置
2. 重新启动服务


### steps:
1. 添加新的机器， 需要指定host和id 
```shell
ansible-playbook add_machine.yml -e "host=xxxx id=x"  -u root
```

2. 所有的机器， 请确保在/etc/ansible/hosts 添加[zoo]和相关的机器ip, 需指定zookeeper的配置
```shell
ansible-playbook start_zoo.yml -e "zoo_cfg=/Users/home/git/playbooks/zookeeper/zoo.cfg" -u root
``` 


