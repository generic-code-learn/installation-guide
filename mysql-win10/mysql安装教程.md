# 添加环境变量

```
mysql-5.7.30-winx64\bin
```

# 添加配置文件

```
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
# 切记此处一定要用双斜杠\\
basedir=D:\\application\\mysql-5.7.30-winx64
# 设置mysql数据库的数据的存放目录
datadir=D:\\application\\mysql-5.7.30-winx64\\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8

#开启日志
general_log=1   
#设置日志路径
general_log_file=D:\\application\\mysql-5.7.30-winx64\\mysql.log    
#慢查询
slow-query-log=1
slow_query_log_file=D:\\application\\mysql-5.7.30-winx64\\slow.log
long_query_time=10
```

# 初始化

执行初始化获取到临时密码

```
mysqld --initialize --console
```

# 安装

使用管理员权限执行

```
mysqld --install
```

# 启动

```
net start mysql
```

# 登录并修改密码

```
alter user user() identified by 'admin';
flush privileges;
```

