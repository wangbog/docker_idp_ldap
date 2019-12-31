# docker_idp_ldap
1. 配置宿主机环境

配置本机IP

修改主机域名 vi /etc/hostname 及 hostname命令

关闭SELinux

开放本机端口（如firewall-cmd）

设置时间同步（NTP配置）

2. 配置Docker环境

sudo yum -y install -y yum-utils device-mapper-persistent-data lvm2

sudo yum -y install docker-ce docker-ce-cli containerd.io

sudo systemctl start docker

可以用hello-world docker镜像验证一下环境： sudo docker run hello-world

git clone https://github.com/carsi-cernet/docker_idp_ldap.git

cd docker_idp_ldap

docker build --rm -t local/idp-cas-zl .

docker run -itd -v /opt/shibboleth-idp/:/opt/shibboleth-idp/ -v /etc/localtime:/etc/localtime:ro -v /etc/hostname:/etc/hostname -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 -p 443:443 -p 8443:8443 --privileged=true local/idp-cas-zl

查询container_id:

docker ps -a

进入该镜像的bash环境：

docker exec -it <container_id> /bin/bash

如需停止容器：

docker stop <container_id> - 停止docker daemon

