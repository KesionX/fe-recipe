# docker

## 国内镜像配置
```
//1.vim /etc/docker/daemon.json
//2.输入下面的json
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
//3. 更新配置重启服务
// systemctl daemon-reload 
// systemctl restart docker
```
