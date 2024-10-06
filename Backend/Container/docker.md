# Docker

Mac上docker的安装命令：

```
brew install --cask --appdir=/Applications docker
```



设置时间：

```
#第一种方式(推荐)：
environment:
  TZ: Asia/Shanghai
  
#第二种方式：
environment:
  SET_CONTAINER_TIMEZONE=true
  CONTAINER_TIMEZONE=Asia/Shanghai

#第三种方式：
volumes:
  - /etc/timezone:/etc/timezone
  - /etc/localtime:/etc/localtime
  
```



