
zipkin 安装
sudo docker run -it -p 9411:9411 -e STORAGE_TYPE=mysql -e MYSQL_DB=tgcloud_zipkin -e MYSQL_HOST=192.168.164.130 -e MYSQL_USER=root -e MYSQL_PASS=123456 -e RABBIT_ADDRESSES=192.168.164.130:5672 -e RABBIT_USER=admin -e RABBIT_PASSWORD=admin openzipkin/zipkin

xxl-job 安装
docker run -e PARAMS="--spring.datasource.url=jdbc:mysql://192.168.164.130:3306/xxl-job?Unicode=true&characterEncoding=UTF-8 --server.port=8011 --spring.datasource.username=root --spring.datasource.password=123456" -p 8011:8011 -v /home/hadoop/xxl-job-admin/applogs:/data/applogs --name xxl-job-admin -d xuxueli/xxl-job-admin:2.0.0

安装 RabbitMQ
apt-get install rabbitmq-server  #安装成功自动启动
查看 RabbitMq状
systemctl status rabbitmq-server   #Active: active (running) 说明处于运行状态

启动、停止、重启
com.tiger.tgcloud.uac.service rabbitmq-server start    # 启动
com.tiger.tgcloud.uac.service rabbitmq-server stop     # 停止
com.tiger.tgcloud.uac.service rabbitmq-server restart  # 重启

rabbitmq-plugins enable rabbitmq_management   # 启用插件
com.tiger.tgcloud.uac.service rabbitmq-server restart    # 重启

servicecomb-saga 使用
#https://jeremy-xu.oschina.io/2018/07/servicecomb-saga%E5%BC%80%E5%8F%91%E5%AE%9E%E6%88%98/
获取源码：
$ git clone https://github.com/apache/incubator-servicecomb-saga.git
$ cd incubator-servicecomb-saga
构建mysql的可执行文件：
$ mvn clean install -DskipTests -Pmysql
创建数据库
创建数据库并给予用户访问该数据库的权限
$ mysql
mysql> create database saga default character set utf8;
mysql> GRANT ALL PRIVILEGES ON saga.* to 'saga'@'localhost' identified by '123456';
mysql> flush priveleges;
mysql> exit
启动alpha-server