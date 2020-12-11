# Docker安装宝塔

## 下载centos
```
docker pull centos
```

## 启动centos
```
docker run -itd --name centos -p 20:20 -p 21:21 -p 80:80 -p 443:443 -p 888:888 -p 8888:8888 -d centos
```

## 增加文件映射
```
docker run -i -t -d -p 8888:8888 -p 888:888 -p 80:80 -p 3306:3306 --privileged=true -v /Users/poison/Sites:/wwwroot --name=centos centos:8 /usr/sbin/init

```

## 安装宝塔
```
docker exec -it centos bash

yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```