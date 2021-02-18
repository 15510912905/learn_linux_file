1    2     3    4    5     6    7    8     启动设备 
0    1     x    x    x     x    x    x     串行下载，可以通过 USB 烧写镜像文件。 
1    0     0    0    0     0    1    0     SD 卡启动。 
1    0     1    0    0     1    1    0     EMMC 启动。 
1    0     0    0    1     0    0    1     NAND FLASH 启动。

I.MX6U 的 GPIO 一共有 5 组：GPIO1、GPIO2、GPIO3、GPIO4 和 GPIO5;
其中 GPIO1 有 32 个 IO，GPIO2 有 22 个 IO，GPIO3 有 29 个 IO、GPIO4 有 29 个 IO，GPIO5最少，只有 12 个 IO，这样一共有 124 个 GPIO.
命名形式就是“IOMUXC_SW_MUC_CTL_PAD_XX_XX”，后面的“XX_XX”就是 GPIO 命名，
比如：GPIO1_IO01、UART1_TX_DATA、JTAG_MOD、SNVS_TAMPER1 等等
IOMUXC_SW_MUX_CTL_PAD_GPIO1_IO00 0X020E005C
1、使能 GPIO1 时钟 
CCM_CCGR1
2、设置 GPIO1_IO03 的复用功能
IOMUXC_SW_MUX_CTL_PAD_GPIO1_IO03   (ALT0~ALT8)
3、配置 GPIO1_IO03
IOMUXC_SW_PAD_CTL_PAD_GPIO1_IO03   (速度设置、驱动能力设置、压摆率设置)
IOMUXC_SW_MUX_CTL_PAD_XX_XX  和 IOMUXC_SW_PAD_CTL_PAD_XX_XX  这两种寄存器都是配置 IO 的，注意是 IO！不是 GPIO，GPIO 是一个 IO 众多复用功能中的一种。
4、设置 GPIO
GPIO1_DR  
当 GPIO 被配置为输出功能以后，向指定的位写入数据那么相应的 IO 就会输出相应的高低电平，比如要设置 GPIO1_IO00 输出高电平，那么就应该设置 GPIO1.DR=1。
当 GPIO被配置为输入模式以后，此寄存器就保存着对应 IO 的电平值，每个位对对应一个 GPIO
GPIO1_GDIR
如果要设置 GPIO 为输入的话就设置相应的位为 0，
如果要设置为输出的话就设置为 1。
GPIO1_PSR
读取相应的位即可获取对应的 GPIO 的状态，也就是 GPIO 的高低电平值。功能和输入状态下的 DR 寄存器一样。
GPIO1_ICR1
GPIO1_ICR2
接下来看 ICR1 和 ICR2 这两个寄存器，都是中断控制寄存器，ICR1 用于配置低 16 个 GPIO，ICR2 用于配置高 16 个 GPIO
GPIO1_IMR
中断屏蔽寄存器,IMR 寄存器用来控制 GPIO 的中断禁止和使能，
如果使能某个 GPIO 的中断，那么设置相应的位为 1 即可，
反之，如果要禁止中断，那么就设置相应的位为 0 即可。
GPIO1_ISR
中断状态寄存器
GPIO1_EDGE_SEL
如果相应的位被置 1，那么就相当与设置了对应的 GPIO 是上升沿和下降沿(双边沿)触发。
I.MX6U GPIO 时钟使能,CMM 有 CCM_CCGR0~CCM_CCGR6 这 7 个寄存器，这 7 个寄存器控制着 I.MX6U 的所有外设时钟开关.
5、控制 GPIO 的输出电平
GPIO1_DR