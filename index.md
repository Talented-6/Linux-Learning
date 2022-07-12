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
```