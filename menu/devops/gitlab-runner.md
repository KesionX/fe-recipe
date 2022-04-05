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
### token
![image](https://user-images.githubusercontent.com/15847900/161719479-aff7acf3-f2ae-4d8d-b7c4-38cdd5fce9d5.png)
token获取请看上图

### tag 配置
tag与commit相关，用于触发ci

![image](https://user-images.githubusercontent.com/15847900/161741572-0b72e6c6-2602-4b14-87e8-9e408ca97082.png)


## 特定分支触发ci

配置job rules

```
rules:
  - if: $CI_COMMIT_BRANCH == "main"
```

```
test-job1:
  stage: test
  rules:
    - if: $CI_COMMIT_BRANCH == "main"
  script:
    - echo "This job tests something"
```




