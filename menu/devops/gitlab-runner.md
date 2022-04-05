# gitlab-runner

## docker-compose 安装
请看[gitlab](./gitlab.md)

## docker gitlab-runner 安装
新建yml：
```
vim /home/data/gitlab/docker-compose.yml
```
内容：
```
version: '3.1'
services:
  gitlab-runner:
    image: 'gitlab/gitlab-runner:latest'
    container_name: 'gitlab-runner'
    restart: always
    volumes:
      - '/srv/gitlab-runner/config:/etc/gitlab-runner'
      - '/var/run/docker.sock:/var/run/docker.sock'
```
运行：
```
docker-compose -f ./docker-compose.yml up -d
```

## 注册
```
docker exec -it gitlab-runner gitlab-runner register
```
之后按提示选择配置
![image](https://user-images.githubusercontent.com/15847900/161719479-aff7acf3-f2ae-4d8d-b7c4-38cdd5fce9d5.png)
token获取请看上图

