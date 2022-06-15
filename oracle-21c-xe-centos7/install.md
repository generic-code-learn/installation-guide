# 一、安装Oracle21c-XE

## 准备rpm

在非OralceLinux环境下安装，需要下载对应平台的rpm

```
https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/index.html
```

在该页面搜索对应的rpm包并下载，如安装21c-xe则搜索 `21c`

## 安装rpm

上传`oracle-database-preinstall-21c-1.0-1.el7.x86_64.rpm`、`oracle-database-xe-21c-1.0-1.ol8.x86_64.rpm`至/opt目录下

切换至/opt目录下，依次执行

```bash
yum -y localinstall oracle-database-preinstall-21c-1.0-1.el7.x86_64.rpm
yum -y localinstall oracle-database-xe-21c-1.0-1.ol8.x86_64.rpm 
```

## 创建实例

```bash
/etc/init.d/oracle-xe-21c configure
```

## 添加环境变量

```bash
vi ~/.bashrc
```

在尾部追加

```bash
export ORACLE_HOME=/opt/oracle/product/21c/dbhomeXE
export ORACLE_SID=ORCLCDB
export PATH=$ORACLE_HOME/bin:$PATH
```

使环境变量生效

```bash
source ~/.bashrc
```

## 注意事项

### oracle服务停止

在服务器重启后oracle监听和服务会停止，需要启动监听和启动数据库

切换至oracle用户

```bash
su oracle
```

启动监听

```bash
lsnrctl start
```

启动数据库

```bash
# 登录sys
sqlplus sys as sysdba
# 启动数据库
startup
# 切换可插拔数据库
alter session set container = xepdb1;
# 启动可插拔数据库
startup
```



> 参考命令：
>
> ```bash
> # 启动监听
> lsnrctl start
> # 停止监听
> lsnrctl stop
> # 查看监听
> lsnrctl stat
> ```

### sqlplus乱码

```bash
1.首先要看一下当前的编码是什么
SQL> select userenv('language') from dual;
 
USERENV('LANGUAGE')
----------------------------------------------------
SIMPLIFIED CHINESE_CHINA.AL32UTF8
 
2.将系统的编码与当前数据库的编码设置成一致
NLS_LANG="SIMPLIFIED CHINESE_CHINA.AL32UTF8"
export NLS_LANG
echo $NLS_LANG
3.写入 ~/.bashrc
4.使生效 source ~/.bashrc
```

### LRM-00109: could not open parameter file '/opt/oracle/dbs/initORCLCDB.ora'

```bash
cp /opt/oracle/admin/XE/pfile/init.ora.5152022141251   /opt/oracle/dbs/initORCLCDB.ora
```



## 卸载

```bash
yum -y remove oracle-database-preinstall-21c-1.0-1.el7.x86_64.rpm
yum -y remove oracle-database-xe-21c-1.0-1.ol7.x86_64.rpm
```

