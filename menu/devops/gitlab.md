# gitlab搭建

## 背景
打算学习一下工程化的搭建，看了些文章，感觉写的还是比较老，流程有点复杂，最终还是直接在gitlab官网上找了docker的搭建方式，不用1分钟就完事了。

## 硬件配置
阿里云 2vcpu、8gib内存，建议使用 2vcpu 4gib以上的，最开始我用 1vcpu 4gib搭建过程中就直接卡死了，从监控上看应该是内存不够，云盘bps直线飙升。

## 安装docker
直接看这个教程吧：https://blog.csdn.net/huyaowei789/article/details/106329204

## 搭建gitlab

### 环境变量

``` shell
vim /etc/proflie
```
加上
``` shell
export GITLAB_HOME=/srv/gitlab
```
配置文件权限
```
mkdir -p /srv/gitlab
chmod +x /srv/gitlab
```

### docker-compose 安装
1. 先安装pip
2. 安装docker-compose
3. vim /home/data/gitlab/docker-compose.yml
```
version: '3.6'
services:
  web:
    image: 'gitlab/gitlab-ee:latest'
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://gitlab.example.com'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '80:80'
      - '443:443'
      - '22:22'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'
```

4. 启动
```
docker-compose -f ./docker-compose.yml up -d
```

5. 打开对应端口的浏览器

6. 如果出现502，很有可能是内存不够，可以等个10分钟再试下
7. 刷新页面查看

## 初始密码
管理员账号：root
管理员密码：所在位置，只有24小时的保质期，记得及时修改密码
```
cat /srv/gitlab/config/initial_root_password
```

