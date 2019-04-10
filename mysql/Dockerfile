FROM mysql:5.7
LABEL MAINTAINER="2775147135@qq.com"
ENV TZ "Asia/Shanghai"
COPY config/my.cnf /etc/mysql/my.cnf






Usage:
#创建你本机中mysql的数据文件的路径
    mkdir /opop
#创建容器
    docker run --name mysql -p 8800:3306 -v /opop:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -itd mysql:5.7
#================== 可选项 =========================
#进入MySQL容器
    docker exec -it <Container_ID> /bin/bash
#进入MySQL实例(密码为123456)
    mysql -uroot -p    
#================== 可选项 =========================
