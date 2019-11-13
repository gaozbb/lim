# Linux常用命令大全
[toc]
## 系统信息
~~~
arch									   显示机器的处理器架构
uname -m						   显示机器的处理器架构
uname -r							 显示正在使用的内核版本
dmidecode -q				   显示硬件系统部件
cat /proc/cpuinfo			 显示CPU info的信息
cat /proc/meminfo		  校验内存使用
cat /proc/version			  显示内核的版本
cal 年份								  显示哪一年 的日历表
date 时间							    11102040201940（月日时分年秒）
~~~

## 关机
~~~
shtdown -h now				关闭系统
init 0									   关闭系统
telinit 0								 关闭系统
shutdown -h hours：minutes	定时关机
shutdown -c						取消定时关机
shutdown -r now			   重启
reboot								   重启
logout								   注销
~~~

## 文件和目录
~~~
cd /home						进入home目录
cd ..									返回上一级目录
cd ../..							   返回上两级目录
cd										 进入个人主目录
cd -									返回上次所在的目录
pwd									  显示工作路径
ls										   查看目录中的文件
ls -F									 查看目录中的文件
ls -l									   显示文件和目录的详细资料
ls -a									  显示隐藏文件
ls *[0~9]*							 显示包含数字的文件名和目录名
tree									  显示文件和目录由根目录开始的树形结构
mkdir dir1						   创建一个叫dir1的目录
mkdir dir dir1				    创建两个叫dir dir1目录
rm -f file							   删除一个file文件
rmdir dir							 删除一个叫dir的目录
rm -rf dir							   删除一个叫做dir的目录并同时删除其内容
rm -rf dir1 dir2				 删除两个目录
mv dir1 new_dir				重命名/移动 一个目录
cp file1 file2						复制一个文件
cp dir/* .								复制一个目录下所有的文件到当前工作目录
cp -a 目录 .							复制一个目录到当前工作目录
cp -r dir dir1						 复制一个目录及子目录
ln -s										创建软连接
ln											  创建硬链接
~~~

### 文件搜索
~~~
find / -name file				开始进入根文件系统搜索文件和目录
find / -user user1				搜索属于用户'user1'的文件和目录
find /home -name \*.bin				在目录home中搜索带有.bin结尾的文件
find /usr/bin -type f -atime +100			搜索过去100天从未被使用过的执行文件
find /usr/bin -type f -mtime -10			搜索子10天内被创建或者修改过的文件
~~~

### 查看文件内容
~~~
cat file							从第一个字节开始正向查看文件内容
tac file							从最后一行开始反向查看一个文件内容
more file							查看一个长文件内容
less file							允许子啊文件中和正向错做一样的反向操作
head -2 file					查看文件的前两行
tail -2 file						查看文件的最后两行
~~~