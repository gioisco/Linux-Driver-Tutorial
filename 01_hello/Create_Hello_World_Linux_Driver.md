# Create a 'Hello World' Linux Driver


## Create Your First Kernel Module!

A kernel module is a piece of software that runs in **kernel space**.  
This is the right environment for device drivers.

### Advantages:
 - Direct access to hardware.

### Disadvantages:
 - Floating-point operations are not supported out of the box.
 - Kernel stack size is smaller compared to user space.

## Let's code!

1. Create a new folder called `01_hello` and add two files inside it:  
   - `hello.c` - This will contain your first kernel module code.  
   - `Makefile` - Instructions to build the module.

---

### **hello.c**
```c
#include <linux/module.h>
#include <linux/init.h>

int my_init(void)
{
	printk("hello - Hello, kernel!\n");
	return 0;
}

void my_exit(void)
{
	printk("hello - Goodbye, kernel!\n");
}

module_init(my_init);
module_exit(my_exit);

MODULE_LICENSE("GPL");
```

---

### **Makefile**
```makefile
obj-m += hello.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

2. Build the kernel module with:

```bash
make
```

It will create a bouce of files. The main important is `hello.ko`, the kernel module.

---

## Insert Your First Kernel Module

1. Open two terminal windows.

2. In the first terminal, monitor the kernel logs:

```bash
sudo dmesg -W
```

3. In the second terminal, insert the kernel module:

```bash
sudo insmod hello.ko
```

This will call the `my_init` function.  

4. Check the first terminal:  
You should see the following message in the kernel logs:

```text
[ 6437.639379] hello - Hello, kernel!
```

5. Confirm the module is inserted by running:

```bash
lsmod | grep hello
```

---

## Remove Your First Kernel Module

1. In the second terminal, remove the kernel module:

```bash
sudo rmmod hello.ko
```

This will call the `my_exit` function, removing the kernel module.

2. Confirm the module is removed by running:

```bash
lsmod | grep hello
```

No output will be displayed.
