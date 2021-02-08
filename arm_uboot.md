T530 ipaddr:192.168.10.25
VMware Network:192.168.10.100
imx6ull ipaddr:192.168.10.200

setenv ipaddr 192.168.10.200
setenv ethaddr 00:04:9f:04:d2:66

setenv serverip 192.168.10.100
saveenv

setenv gatewayip 192.168.10.1 
setenv netmask 255.255.255.0 
setenv serverip 192.168.10.200 
saveenv 

reset

fatls mmc 1:1               /* 查询EMMC设备号为1分区1中的所有的目录和文件 */

/* 从网络启动Linux */
setenv bootcmd 'tftp 80800000 zImage; tftp 83000000 imx6ull-14x14-emmc-7-1024x600-c.dtb; bootz 80800000 - 83000000'
saveenv
boot

/* 自定义变量启动Linux */
setenv test_ipset 'setenv ipaddr 192.168.10.200;setenv ethaddr 00:04:9f:04:d2:66;setenv serverip 192.168.10.100;saveenv'
setenv bootargsmmc_net 'setenv bootargs console=ttymxc0,115200 root=/dev/nfs rw nfsroot=192.168.10.100:/home/wuqian/linux/nfs/rootfs ip=192.168.10.200:192.168.10.100:192.168.10.1:255.255.255.0::eth0:off'
setenv bootcmdmmc_net 'tftp 80800000 zImage;tftp 83000000 imx6ull-14x14-emmc-7-1024x600-c.dtb; bootz 80800000 - 83000000'
setenv test_mmcbootz 'run test_ipset;run bootargsmmc_net;run bootcmdmmc_net'
saveenv

/* 从EMMC启动Linux */
setenv bootcmd 'fatload mmc 1:1 80800000 zImage; fatload mmc 1:1 83000000 imx6ull-14x14-emmc-7-1024x600-c.dtb; bootz 80800000 - 83000000'
savenev
boot

bootcmd=run findfdt;mmc dev ${mmcdev};mmc dev ${mmcdev}; if mmc rescan; then if run loadbootscript; then run bootscript; else if run loadimage; then run mmcboot; else run netboot; fi; fi; else run netboot; fi

/* 通过自定义环境变量来实现不同的启动方式 */
mfgtool_args=setenv bootargs console=${console},${baudrate} rdinit=/linuxrc g_mass_storage.stall=0 g_mass_storage.removable=1 g_mass_storage.file=/fat g_mass_storage.ro=1 g_mass_storage.idVendor=0x066F g_mass_storage.idProduct=0x37FF g_mass_storage.iSerialNumber="" clk_ignore_unused 
mmcargs=setenv bootargs console=${console},${baudrate} root=${mmcroot}
netargs=setenv bootargs console=${console},${baudrate} root=/dev/nfs ip=dhcp nfsroot=${serverip}:${nfsroot},v3,tcp
run mfgtool_args
run mmcargs
run netargs

/* 原始uboot环境变量 */
/*
baudrate=115200
board_name=EVK
board_rev=14X14
boot_fdt=try
bootcmd=run findfdt;mmc dev ${mmcdev};mmc dev ${mmcdev}; if mmc rescan; then if run loadbootscript; then run bootscript; else if run loadimage; then run mmcboot; else run netboot; fi; fi; else run netboot; fi
bootcmd_mfg=run mfgtool_args;bootz ${loadaddr} ${initrd_addr} ${fdt_addr};
bootdelay=3
bootscript=echo Running bootscript from mmc ...; source
console=ttymxc0
ethact=FEC1
ethprime=FEC
fdt_addr=0x83000000
fdt_file=imx6ull-14x14-emmc-7-1024x600-c.dtb
fdt_high=0xffffffff
findfdt=if test $fdt_file = undefined; then if test $board_name = EVK && test $board_rev = 9X9; then setenv fdt_file imx6ull-9x9-evk.dtb; fi; if test $board_name = EVK && test $board_rev = 14X14; then setenv fdt_file imx6ull-14x14-evk.dtb; fi; if test $fdt_file = undefined; then echo WARNING: Could not determine dtb to use; fi; fi;
image=zImage
initrd_addr=0x83800000
initrd_high=0xffffffff
ip_dyn=yes
loadaddr=0x80800000
loadbootscript=fatload mmc ${mmcdev}:${mmcpart} ${loadaddr} ${script};
loadfdt=fatload mmc ${mmcdev}:${mmcpart} ${fdt_addr} ${fdt_file}
loadimage=fatload mmc ${mmcdev}:${mmcpart} ${loadaddr} ${image}
logo_file=alientek.bmp
mfgtool_args=setenv bootargs console=${console},${baudrate} rdinit=/linuxrc g_mass_storage.stall=0 g_mass_storage.removable=1 g_mass_storage.file=/fat g_mass_storage.ro=1 g_mass_storage.idVendor=0x066F g_mass_storage.idProduct=0x37FF g_mass_storage.iSerialNumber="" clk_ignore_unused 
mmcargs=setenv bootargs console=${console},${baudrate} root=${mmcroot}
mmcautodetect=yes
mmcboot=echo Booting from mmc ...; run mmcargs; if test ${boot_fdt} = yes || test ${boot_fdt} = try; then if run loadfdt; then bootz ${loadaddr} - ${fdt_addr}; else if test ${boot_fdt} = try; then bootz; else echo WARN: Cannot load the DT; fi; fi; else bootz; fi;
mmcdev=1
mmcpart=1
mmcroot=/dev/mmcblk1p2 rootwait rw
netargs=setenv bootargs console=${console},${baudrate} root=/dev/nfs ip=dhcp nfsroot=${serverip}:${nfsroot},v3,tcp
netboot=echo Booting from net ...; run netargs; if test ${ip_dyn} = yes; then setenv get_cmd dhcp; else setenv get_cmd tftp; fi; ${get_cmd} ${image}; if test ${boot_fdt} = yes || test ${boot_fdt} = try; then if ${get_cmd} ${fdt_addr} ${fdt_file}; then bootz ${loadaddr} - ${fdt_addr}; else if test ${boot_fdt} = try; then bootz; else echo WARN: Cannot load the DT; fi; fi; else bootz; fi;
panel=ATK-LCD-7-1024x600
script=boot.scr
splashimage=0x88000000
splashpos=m,m

Environment size: 2534/8188 bytes
*/