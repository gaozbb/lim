> 目录，磁盘，权限


[toc]

## 文件处理命令

### 目录处理命令
~~~
ls								  查看文件
ls -a							    查看所有文件
ls -l								 查看文件获取详细信息
ls -lh							查看文件带大小有单位
ls -ld							查看目录信息
ls -i								  查询任何一个文件i节点
~~~

### 文件处理命令

```
touch						创建文件
cat								查询文件内容
tac								显示文件内容（倒着显示）
more							分页显示文件内容
less							   分页显示文件内容（可以向上翻页）
head -n					  显示文件前几行
tail -n						  显示文件末尾几行
tail -f							动态显示文件末尾内容
```

**软链接和硬链接**
~~~
ln -s								创建软连接
软链接特征，类似Windows快捷方式
ln								  创建硬链接
硬链接特征，拷贝cp -p + 同步更新
~~~

### 权限管理命令
~~~
chmod +-=修改权限
r			4
w		   2
x			 1
chmod +R 递归修改

chown
~~~
> r			读权限			r:ls
> w		   写权限			w:/touch/mkdir/rmdir/rm
> x			执行权限		x:cd

### 文件搜索命令
* find
~~~
find /路径 -name init					搜索
find /路径 -size +204800			查找大于100mb的文件
find /home -user xxx				查找所有者为xxx的文件
find /路径 -cmin -5					查找五分钟内被修改过的属性文件和目录
find /路径	-size +163840 -a -size -204800			查找大于80MB小于100MB的文件
find /路径	-name	init*	-a	-type	d					查找文件下所有的目录
find /路径 -user xx	-ok	rm {} \;				删除所有用户名xx的文件并询问是否
find .	-inum i节点	-exec rm	{}	\;			删除当前目录下的i节点文件

-a		两个条件同时被满足
-o		两个条件满足任意一个
-amin	访问时间		access
-cmin	文件属性		change
-mmin	文件内容		modify

f文件				d目录			l软链接文件

1数据块=512字节		0.5k
1MB=1024KB
~~~
* locate
~~~
updatedb		更新文件资料库
locate -i			不区分大小写查找
~~~

### 帮助命令
~~~
man 				查看命令或配置文件帮助信息
whatis				看命令简短信息
apropos				获得配置文件相关信息
命令 --help		获得命令主要选项信息
man date		查看日期参数
help					查看shell内置命令
~~~

### 用户管理命令
~~~
useradd
passwd

who查看登录用户信息
w		查看当前登录用户详细信息
~~~

### 压缩解压命令
~~~
.gz
gzip		压缩
gunzip		解压缩

tar		打包
tar -zcf	文件名.tar 文件名			打包目录
tar -zxvf	文件名.tar 文件名			解包

zip xx.zip xx							压缩.zip
zip -r xx.zip xx						压缩目录

-x			解包
-v			显示详细信息
-f			指定解压文件
-z			解压缩
~~~

### 网络命令
~~~
 wall 			发送广播信息
 ping 			测试网络连通性（可以加-c里面附带次数）
 ifconfig		查看和设置网卡信息
 mail 用户名			发送邮件
 ctrl + d			保存发送
 mail 				查看邮件
 last					列出目前和过去登入系统的用户信息
 lastlog			检查某特定用户上次登录的时间
 traceroute 网址			显示数据包到主机间的路径
 
 netstat			显示网络相关信息
 netstat -tlun						查看本机监听的端口
 netstat -an						查看本机所有的网络连接
 netstat -rn						查看本机路由表
 
 setup									配置网络
 
 mount								挂载命令
 mount [-t 文件系统]	设备文件名	挂载点
 
 -t						TCP协议
 -u						UDP协议
 -l						监听
 -r						路由
 -n						显示IP地址和端口号
 
~~~
### 关机重启命令
~~~
shutdown -h 时间				指定时间关机
shutdown -r	时间				 指定时间重启
shutdown -c							取消前一个关机命令
其他关机命令：
halt
poweroff								相当于直接断电
init 0
重启命令：
reboot
init 6
~~~
**系统运行级别**
> 0						关机
> 1						单用户
> 2						不完全用户，不含NFS服务
> 3						完全多用户
> 4						未分配
> 5						图形界面
> 6						重启
> 
> 修改系统默认运行级别
> id:3:initdefault:
> 查询系统运行级别
> runlevel
> 退出登录命令
> logout



## 软件包管理

### 软件包
1.软件包分类
* 源码包
	* 源码安装包
* 二进制包（RPM包、系统默认包）

2.源码包
***优点：***
* 开源
* 可以自由选择需要的功能
* 软件是编译安装
* 卸载方便

***缺点***
* 安装步骤多
* 编译时间较长
* 容易报错，很难解决

3.RPM包
***二进制包优点***
* 管理系统简单
* 安装速度比源码包快

***二进制包缺点***
* 看不到源代码
* 功能选择不如源代码包灵活
* 依赖性高

### rpm命令管理
1.rpm包命名原则
~~~
httpd-2.2.15-15.e16.centos.1.i686.rmp
httpd					软件包名
2.2.15					软件版本
15						   软件发布次数
e16.centos				适合的LInux平台
i686						适合的硬件平台
rpm						rpm包扩展名
~~~
2.RPM包依赖性
* 树形依赖					a-b-c
* 环形依赖					a-b-c-a
* 模块依赖					www.rpmfind.net

3.包全名与包名
*包全名：操作的没有安装的软件包，使用包全名
* 包名：操作已安装的软件包，使用包名
4.RPM安装
~~~
rpm -ivh 包全名
-i（install）				安装
-v（verbose）			显示详细信息
-h（hash）					显示进度
--nodeps						不检测依赖性
~~~
5.RPM包升级
> rpm -Uvh	包全名
> -U(upgrade)			升级

6.卸载
> rpm -e 包名
> -e(erase)				卸载
> --nodeps				不检查依赖性

7.查询
~~~
1.查询是否安装
rpm -q	包名			查询包是否安装
-q（query）			查询
-a（all）					所有
2.查询软件包详细信息
rpm -qi 包名
-i（informatiion）		查询软件信息
-p（package）				  查询未安装包信息
3.查询包中文件安装位置
rpm -ql 包名
-l（list）							列表
-p（package）				查询未安装包信息
4.查询系统文件属于哪个RPM包
rpm -qf 系统文件名
5.查询软件包的依赖性
rpm -qR 包名
-p（package）					查询未安装包信息
~~~
8.校验
~~~
rpm -V	已安装的包名
验证内容中的八个信息
S			文件大小是否改变
M			文件类型或文件的权限是否改变
5			文件MD5校验和是否改变（文件内容是否改变）
D			设备的中，从代码是否改变
L			文件路径是否改变
U			文件的所有者是否改变
G			文件的属组是否改变
T			文件的修改时间是否改变

c			配置文件
d			普通文档
g			该文件不应该被这个RPM包包含
l			授权文件
r			描述文件


RPM包中文件提取
rpm2cpio 包全名 | \
cpro -idv . 文件绝对路径
-i				还原
-d				还原是自动新建目录
-v				显示还原过程
~~~

## 用户和用户组

### 用户信息文件
~~~
/etc/passwd
第一个字段 用户名称
第二个阶段 密码标志
第三个阶段 UID
第四个字段 GID（用户初始组ID）
第五个字段 用户说明
第六个字段 家目录
	普通用户：/home/用户名/
	超级用户：/root/
第七个字段 登陆之后的Shell
~~~

### 影子文件
~~~
/etc/shadow
第一个字段 用户名称
第二个字段 加密密码
	加密算法SHA512撒列加密算法
	如果密码位是“!!”或“*”代表没有密码
第三字段 密码最后一次修改日期
	1970年1月1日为标准时间，每过一天加一
第四字段 两次密码修改时间间隔
第五字段 密码有效期（和第三字段相比）
第六字段 密码修改到期前警告的天数
第七字段 密码到期之后的宽限天数
第八字段 账号失效时间
第九字段 保留

~~~

### 用户配置文件
~~~
组信息文件 /etc/group
第一字段 组名
第二字段 组密码标志
第三字段 GID
第四字段 组中附加用户

组密码文件 /etc/gshadow
第一字段 组名
第二字段 组密码
第三字段 组管理员用户名
第四阶段 组中附加用户
~~~

### 用户管理相关文件
~~~
用户的家目录
	普通用户：/home/用户名/，所有者和所属组都是此用户，权限是700
	超级用户：/root/，所有者和所属组都是root用户，权限是550
用户的邮箱
	/var/spool/mail/用户名/
用户模板目录
	/etc/skel/s
~~~

### 用户管理命令
~~~
useradd命令
-u UID					手工指定用户的UID号
-d 家目录				手工指定用户的家目录
-c 用户说明				手工指定用户的说明
-g 组名					手工指定用户的初始组
-G 组名					指定用户的附加组
-s shell					手工指定用户的登录shell，默认是/bin/bash

useradd sc				添加默认用户
grep sc /etc/passwd
grep sc /etc/shadow
grep sc /etc/group
grep sc /etc/gshadow
ll -d /home/sc/
ls /var/spool/mail/lamp


passwd [选项] 用户名
-S		查询用户密码的密码状态，仅root可用
-l		暂时锁定用户
-u		解锁用户
--stdin		可以通过管道符输出的数据作为用户的密码
~~~