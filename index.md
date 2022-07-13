# 三种网络连接方式
* 桥接——每个虚拟系统都分配一个ip
* NAT（虚拟地址转换）——内网和外网在不同网段，不造成网络冲突
* 主机模式——独立的系统
# Fedora SSH Root登录
```
sudo passwd root
sudo vi /etc/ssh/sshd_config (PermitRootLogin yes)
sudo service sshd restart
ps -au|grep sshd
```
# 关机 重启 注销
```
shutdown -h now (halt)
shutdown -h 1 (单位为分钟)
shutdown -r now (reboot)
halt
reboot
sync (把内存的数据同步到磁盘) (最好先执行一次再关机或重启)

su - <用户名> (switch user)(root到普通用户不用输入密码)
logout 在图形界面下等于exit，实质无效，在运行级别3(多用户无界面)下有效
```
# 多用户
```
useradd (-d <Home-Direcotry>) (-g <User-Group>) <UserName> 默认切换到家目录
userdel (-r) <UserName> 是否删掉用户目录
# group 与上面同式，默认单用户单组
usermod (-g <User-Group>) <User-Name>
passwd <UserName> 如果不加用户名修改的是当前用户的密码
pwd (Print Working Directory)
who am i/whoami (前者显示当前用户的信息更全)(前者在GUI下无效)
id (uid gid group)
```
> /etc/shadow    /etc/passwd /etc/groupo

# 运行级别
```
0 关机
1 单用户 [找回密码]
2 多用户无网络
3 多用户有网络
4 系统未使用保留给用户
5 图形界面
6 系统重启

init [0/1/2/3/4/5/6]

systemctl get-default
systemctl set-default multi-user.target/graphical.target
```
# 找回root密码
```
rhgb quiet -> rd.break enforcing=0
mount -o remount,rw /sysroot
chroot /sysroot
passwd
exit

restorecon -v /etc/shadow
setenforce 1
```
# 帮助指令
```
man [命令或配置文件]
help 
```
# 文件目录系统
```
mkdir (-p) <Directory-Name> (p代表多级目录)
rmdir -rf
rm -rf (recursion force)
cp (-r) <source> <tartget>
\cp （原始命令）强制覆盖不提示
cat -n | more 显示行号
more 和 less都可以单独使用，less更适合大文件的读取
echo输出内容到控制台
head -n 5 <File> 默认查看前10行
tail -n 5 默认显示后10行
tail -f 追踪文件的变化
> 输出重定向(覆盖)
>> 追加
软链接(快捷方式)(符号链接)(pwd不显示为目标)
history (<number>)查看用过的历史命令  histroy | head -10 (history在fish不便使用) (!行数执行先前执行过的命令)(!!执行最后执行的命令)
```
# 时间日期类型
```
date 
+%Y年份 %m月份 %d天 %H %M %S 
date "+%Y-%m-%d %H:%M:%S"
date -s "2022-7-12 20:01:03 # 设置时间
cal (<Year>)显示日历
```
# 查找指令
```
find [搜索目录] [选项--name --user -size<+n大于-n小于n等于>]
updatedb -> locate  (管理员需要定期更新数据库)
which 查看某个指令在哪个目录下
‘|’，表示将前一个命令的处理结果输出传递给后面的命令处理
grep <-n显示行号/i忽略字母大小写> 
```
# 压缩和解压
```
gzip 压缩解压缩 gunzip解压
zip(-r 递归压缩) unzip(-d 指定解压后文件的存放目录) (/home/*仍是将home目录也压缩，而不是只压缩子目录)
tar 打包指令(-c 产生打包文件，-v显示详细信息，-f指定压缩后的文件名，-z使用gzip指令，-x解包提取extract, tar文件，-C指定解压后的路径(跟在末尾且必须确保文件夹存在)) 压缩-zcvf 解压-zxvf  (打包压缩要在相对路径下压缩)
```
# 组管理和文件管理
    所有者(owner) 所在组(group) 其他组()
    chown <User-Name> <File-Name> 改变所有者
    groupadd
    useradd -g <Group-Name> <User-Name>
    chgrp <Group-Name> <File-Name> 改变所在组
    usermod -d <Directory-Name> <User-Name> 用户要有进入这个目录的权限

    -rw-r--r-- (第0位确定文件类型 l链接 d目录 c字符设备文件 b块设备 -文件)(r read w write x execute)
- rwx作用到`文件`。w表示可以修改，但是不代表可以删除，删除一个文件的前提是对该文件所在目录有w的权限
- rwx作用到`目录`。x代表可以进入该目录。w表示可以在目录内创建删除重命令目录或文件
