1  修改设备树文件 
alphaled { 
	#address-cells = <1>; 
	#size-cells = <1>;  
	compatible = "atkalpha-led"; 
	status = "okay"; 
	reg = < 0X020C406C 0X04       /* CCM_CCGR1_BASE            */ 
			0X020E0068 0X04       /* SW_MUX_GPIO1_IO03_BASE    */ 
			0X020E02F4 0X04       /* SW_PAD_GPIO1_IO03_BASE    */ 
			0X0209C000 0X04       /* GPIO1_DR_BASE             */ 
			0X0209C004 0X04 >;    /* GPIO1_GDIR_BASE           */ 
}; 

设备树修改完成以后输入如下命令重新编译一下
make dtbs 

 /* 获取设备树中的属性数据 */ 
 /* 1、获取设备节点：alphaled */ 
 dtsled.nd = of_find_node_by_path("/alphaled"); 
 if(dtsled.nd == NULL) { 
	 printk("alphaled node can not found!\r\n"); 
	 return -EINVAL; 
 } else { 
	 printk("alphaled node has been found!\r\n"); 
 } 

 /* 2、获取 compatible属性内容 */ 
 proper = of_find_property(dtsled.nd, "compatible", NULL); 
 if(proper == NULL) { 
	 printk("compatible property find failed\r\n"); 
 } else { 
	 printk("compatible = %s\r\n", (char*)proper->value); 
 } 

 /* 3、获取 status属性内容 */ 
 ret = of_property_read_string(dtsled.nd, "status", &str); 
 if(ret < 0){ 
	 printk("status read failed!\r\n"); 
 } else { 
	 printk("status = %s\r\n",str); 
 } 

/* 4、获取 reg属性内容 */ 
 ret = of_property_read_u32_array(dtsled.nd, "reg", regdata, 10); 
 if(ret < 0) { 
	 printk("reg property read failed!\r\n"); 
 } else { 
	 u8 i = 0; 
	 printk("reg data:\r\n"); 
	 for(i = 0; i < 10; i++) 
		 printk("%#X ", regdata[i]); 
	 printk("\r\n"); 
 } 
  
 /* 初始化 LED */  
 IMX6U_CCM_CCGR1 = of_iomap(dtsled.nd, 0); 
 SW_MUX_GPIO1_IO03 = of_iomap(dtsled.nd, 1); 
 SW_PAD_GPIO1_IO03 = of_iomap(dtsled.nd, 2); 
 GPIO1_DR = of_iomap(dtsled.nd, 3); 
 GPIO1_GDIR = of_iomap(dtsled.nd, 4); 
 