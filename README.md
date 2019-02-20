- centos7 一键安装python3.7环境 
    ```shell
      ansible-playbook centos4Py3.yml -e "host=xxxx" -u root
    ```
- 更新group的所有机器的/etc/hosts, ip 和 hostname
    ```shell
      ansible-playbook  update_host.yml -e "group=xxx"  -u root  
    ```