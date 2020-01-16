# TCP_BBR
The original and enhanced BBR implementation

Modified by Yankee@hostloc and nanqinglang.

## Build Instructions

```Bash
wget -O ./tcp_tsunami.c https://raw.githubusercontent.com/KozakaiAya/TCP_BBR/master/Master/tcp_tsunami.c

wget -O ./tcp_tsunami.c https://github.com/superhero75/TCP_BBR/blob/master/tcp_tsunami.c

echo "obj-m:=tcp_tsunami.o" > Makefile
make -C /lib/modules/$(uname -r)/build M=`pwd` modules CC=/usr/bin/gcc
cp tcp_tsunami.ko /lib/modules/$(uname -r)/kernel/drivers/
echo 'tcp_tsunami' | sudo tee -a /etc/modules
depmod
modprobe tcp_tsunami
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=tsunami" >> /etc/sysctl.conf
sysctl -p
```

**Special note for Linux Kernel 4.15 & gcc 7.3**

For some strange reasons, the compiler cannot find necessary header files. Therefore, ```echo "ccflags-y=-I/usr/lib/gcc/x86_64-linux-gnu/7/include" >> Makefile``` is needed.

## Remark

Since Linux Kernel v5.1, `bbrplus` no longer needs to be updated, because most of its ideas have been merged to the mainline kernel.
