# 安装Nginx
- 安装并启动 docker run -d -p 80:80 --name webserver nginx
- 停止 docker stop webserver
- 删除实例 docker rm webserver

# 安装Mysql
- 安装 docker pull mysql:latest
- 启动 docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
- 停止 docker stop mysql
- docker rm mysql
- 进入容器 docker exec -it mysql bash