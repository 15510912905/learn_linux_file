T530 ipaddr:192.168.10.25
VMware Network:192.168.10.100
imx6ull ipaddr:192.168.10.200

ifconfig eth0 up
ifconfig eth0 192.168.10.200
ifconfig
/* 设置静态 ip */
vi /etc/rc.local 
/*
PATH=/sbin:/bin:/usr/sbin:/usr/bin
ifconfig eth0 192.168.10.200 netmask 255.255.255.0
route add default gw 192.168.10.1
echo "nameserver 114.114.114.114" > /etc/resolv.conf
*/

uname -srm     /* 查询版本 */

ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf-


/* 将本地文件复制到远程 */
scp /home/namefile root@192.168.10.200:/home/root/wqfile
scp -r /home/namedir root@192.168.10.200:/home/root/wqfile
/* 将远程文件复制到本地 */
scp root@192.168.10.200:/home/root/ /home/namefile
scp -r root@192.168.10.200:/home/root/ /home/namedir·

/* 更新内核到开发板 */
scp zImage root@192.168.10.200:/run/media/mmcblk1p1/

/* 第一步 */
insmod chrdevbase.ko                      /* 加载驱动 */
modprobe chrdevbase.ko                    /* depmod */
lsmod                                     /* 查看当前系统中存在的模块 */
cat /proc/devices 
/* 第二步 */
mknod /dev/chrdevbase c 200 0             /* 创建设备节点文件 */
ls /dev/chrdevbase -l
/* 第三步 */
./chrdevbaseApp /dev/chrdevbase 1         /* chrdevbase设备操作读测试  */
./chrdevbaseApp /dev/chrdevbase 2         /* chrdevbase设备操作写测试  */
/* 第四步 */
rmmod chrdevbase.ko                       /* 卸载驱动模块 */

uname -srm                         //查看内核版本
ls /dev/sda*                       //查看usb设备
ls /dev/ttyUSB*                    //查看u转串
df -h                              //df命令检查Linux系统磁盘空间                   
lsblk                              //列出块设备 
sudo fdisk -l                      //查看你系统中的所有分区表，包括所有的USB设备
dmesg                              //识别出 USB 设备名
file *name                         //查看文件信息包括架构















Linux的man很强大，该手册分成很多section，使用man时可以指定不同的section来浏览，各个section意义如下： 
1 - commands
2 - system calls
3 - library calls
4 - special files
5 - file formats and convertions
6 - games for linux
7 - macro packages and conventions
8 - system management commands
9 - 其他
解释一下, 
1是普通的命令
2是系统调用,如open,write之类的(通过这个，至少可以很方便的查到调用这个函数，需要加什么头文件)
3是库函数,如printf,fread
4是特殊文件,也就是/dev下的各种设备文件
5是指文件的格式,比如passwd, 就会说明这个文件中各个字段的含义
6是给游戏留的,由各个游戏自己定义
7是附件还有一些变量,比如向environ这种全局变量在这里就有说明
8是系统管理用的命令,这些命令只能由root使用,如ifconfig
想要指定section就直接在man的后面加上数字,比如 :
eg:man ls
man open

