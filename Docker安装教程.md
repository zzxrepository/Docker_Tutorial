> 今天毛毛张分享的是基于CentOS7系统下安装Docker的教程



[toc]

# 1.卸载旧版

- 首先如果系统中已经存在旧的Docker，则先通过下面命令进行卸载：

  ```shell
  yum remove docker \
      docker-client \
      docker-client-latest \
      docker-common \
      docker-latest \
      docker-latest-logrotate \
      docker-logrotate \
      docker-engine \
      docker-selinux 
  ```

# 2.配置Docker的yum库

- 首先要安装一个yum工具：

  ```shell
  sudo yum install -y yum-utils device-mapper-persistent-data lvm2
  ```

- 安装成功后，执行命令，配置Docker的yum源（已更新为阿里云源）：

  ```shell
  sudo yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
  sudo sed -i 's+download.docker.com+mirrors.aliyun.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo
  ```

- 更新yum，建立缓存：

  ```shell
  sudo yum makecache fast
  ```

# 3.安装Docker

- 最后，执行命令，安装Docker：

  ```shell
  yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

# 4.启动和校验

```Bash
# 启动Docker
systemctl start docker

# 停止Docker
systemctl stop docker

# 重启
systemctl restart docker

# 设置开机自启
systemctl enable docker

# 执行docker ps命令，如果不报错，说明安装启动成功
docker ps
```

# 5.配置镜像加速

- 配置镜像加速地址步骤如下：

  ```shell
  # 创建目录
  mkdir -p /etc/docker
  
  # 复制内容
  tee /etc/docker/daemon.json <<-'EOF'
  {
    "registry-mirrors": [
      "https://docker.hpcloud.cloud",
      "https://docker.m.daocloud.io",
      "https://docker.unsee.tech",
      "https://docker.1panel.live",
      "http://mirrors.ustc.edu.cn",
      "https://docker.chenby.cn",
      "http://mirror.azure.cn",
      "https://dockerpull.org",
      "https://dockerhub.icu",
      "https://hub.rat.dev"
    ]
  }
  EOF
  
  # 重新加载配置
  systemctl daemon-reload
  
  # 重启Docker
  systemctl restart docker
  ```

- 镜像加速地址可能会变更，如果失效可以百度找最新的docker镜像，毛毛张在下面附上两个`Docker`镜像源汇总的网站：

  - <https://cloud.tencent.com/developer/article/2471124>

  - <https://www.coderjia.cn/archives/dba3f94c-a021-468a-8ac6-e840f85867ea>


# 6.官网教程

- 最新的安装教程可以查看官网：<https://docs.docker.com/engine/install/centos/>



