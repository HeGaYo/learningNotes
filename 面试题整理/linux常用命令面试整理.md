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
