- linux的内核作用
1. 系统内存管理
虚拟内存 ->  内核(内存页面表) -> 物理内存/交换空间(硬盘)
2. 硬件设备管理
linux内核代码中插入了驱动代码
3. 软件程序管理
init进程负责启动系统上的所有其他进程
用一个表来管理系统开机要启动的进程：/etc/inittab
将启动或者停止某个应用的脚本放在：/etc/init.d/目录下。脚本通过入口/etc/rcX.d目录下的入口启动。
4. 文件系统管理


- linux获取cpu使用率
top
cat /proc/stat
cat /proc/cpuinfo

- linux获取内存使用率
cat /proc/meminfo
free -m

- 查看磁盘空间
df -hl
df命令是linux系统上以磁盘分区为单位来查看文件系统的命令，后面可以加不同的参数来查看磁盘的剩余空间信息
df -hl 查看磁盘剩余空间
du -sm [文件夹] 范围该文件夹总m树

- 查看磁盘分区
fdisk -e

- 查看硬盘剩余空间
df -h

- 查看目录占用空间
du -hs 目录名

- 重命名
mv A B

- 查看系统运行的所有进程
ps -ef

- 显示文件或目录
ls -l 显示一个文件的属性以及文件所属的用户和组
r-4 w-2 x-1

- 修改权限
chgrp
chown
chmod

- 硬链接 软链接
ln -s A B
ln A B

- 目录操作
mkdir
rmdir
cp
rm
pwd 显示当前目录

- 查看文件
cat
head
tail
tail -f 允许在其他进程是用的时候查看这个文件的内容。可以实时监测系统日志。
more
less
nl
file 查看文件类型

- 磁盘管理
df 列出磁盘使用量
du 检查磁盘空间使用量
fdisk 用于磁盘分区

- 查看某个进程的端口号
netstat -nlp | grep dnsmasq
