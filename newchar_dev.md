/* 新的字符设备注册方法 */
1、字符设备结构
struct cdev {
	struct kobject kobj;
	struct module *owner;
	const struct file_operations *ops;
	struct list_head list;
	dev_t dev;
	unsigned int count;
};
2、cdev_init 函数
void cdev_init(struct cdev *cdev, const struct file_operations *fops);
3、cdev_add 函数
int cdev_add(struct cdev *p, dev_t dev, unsigned count);
4、cdev_del 函数
void cdev_del(struct cdev *p)
mdev 来实现设备节点文件的自动创建与删除
echo /sbin/mdev > /proc/sys/kernel/hotplug
5、创建和删除类
struct class *__class_create(struct module *owner, const char *name,struct lock_class_key *key);
struct class *class_create (struct module *owner, const char *name);
void class_destroy(struct class *cls);
6、创建设备
struct device *device_create(struct class *class,struct device *parent,dev_t devt,void *drvdata,const char *fmt, ...);
/* device_create 是个可变参数函数，参数 class 就是设备要创建哪个类下面；参数 parent 是父设备，
一般为 NULL，也就是没有父设备；参数 devt 是设备号；参数 drvdata 是设备可能会使用的一些数据，
一般为 NULL；参数 fmt 是设备名字，如果设置 fmt=xxx 的话，就会生成/dev/xxx这个设备文件。返回值就是创建好的设备。*/
void device_destroy(struct class *class, dev_t devt);
7、设置文件私有数据
/* 设备结构体 */
struct test_dev{
	dev_t devid; /* 设备号 */
	struct cdev cdev; /* cdev */
	struct class *class; /* 类 */
	struct device *device; /* 设备 */
	int major; /* 主设备号 */
	int minor; /* 次设备号 */
};

