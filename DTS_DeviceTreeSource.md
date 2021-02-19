设备树源文件扩展名为.dts
DTB 是将DTS 编译以后得到的二进制文件
将.dts 编译为.dtb需要要用到 DTC 工具
只是编译设备树的话建议使用“make dtbs”
1 .dtsi 头文件
设备树的头文件扩展名为.dtsi
“#include”来引用.h、.dtsi 和.dts 文件
2 .设备节点
设备树是采用树形结构来描述板子上的设备信息的文件，每个设备都是一个节点，
叫做设备节点，每个节点都通过一些属性信息来描述节点信息，属性就是键—值对。

“/”是根节点，每个设备树文件只有一个根节点。

cpu0:cpu@0
“node-name@unit-address”
“node-name”是节点名字
“unit-address”一般表示设备的地址或寄存器首地址，如果某个节点没有地址或者寄存器的话“unit-address”可以不要
label: node-name@unit-address
“label”是节点标签
“node-name”是节点名字
“unit-address”一般表示设备的地址或寄存器首地址，如果某个节点没有地址或者寄存器的话“unit-address”可以不要
引入 label 的目的就是为了方便访问节点，可以直接通过&label 来访问这个节点。
①、字符串
compatible = "arm,cortex-a7";
②、32 位无符号整数
reg = <0>;
③、字符串列表
compatible = "fsl,imx6ull-gpmi-nand", "fsl, imx6ul-gpmi-nand";
3 标准属性
1、compatible 属性
"manufacturer,model"
其中 manufacturer 表示厂商，model 一般是模块对应的驱动名字。
compatible = "fsl,imx6ul-evk-wm8960","fsl,imx-audio-wm8960";
属性值有两个，分别为“fsl,imx6ul-evk-wm8960”和“fsl,imx-audio-wm8960”，其中“fsl”
表示厂商是飞思卡尔，“imx6ul-evk-wm8960”和“imx-audio-wm8960”表示驱动模块名字。sound
这个设备首先使用第一个兼容值在 Linux 内核里面查找，看看能不能找到与之匹配的驱动文件，
如果没有找到的话就使用第二个兼容值查。
2、model 属性
3、status 属性
4、#address-cells 和#size-cells 属性
5、reg 属性
reg 属性前面已经提到过了，reg 属性的值一般是(address，length)对。
6、ranges 属性
ranges属性值可以为空或者按照(child-bus-address,parent-bus-address,length)格式编写的数字矩阵
7、name 属性
8、device_type 属性
4 根节点 compatible 属性
Linux 内核会通过根节点的 compoatible 属性查看是否支持此设备，如果支持的话设备就会启动 Linux 内核。
1、使用设备树之前设备匹配方法
Linux内核都用MACHINE_START和MACHINE_END来定义一个 machine_desc 结构体来描述这个设备，在文件 arch/arm/include/asm/mach/arch.h 中。
当 Linux 内 核 引 入 设 备 树 以 后 就 不 再 使 用 MACHINE_START 了 ， 而 是 换 为 了DT_MACHINE_START。义在文件 arch/arm/include/asm/mach/arch.h里面。
5 向节点追加或修改内容

9 设备树常用 OF 操作函数

