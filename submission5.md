# GitOps & SRE Lab

## Task 1: Key Metrics for SRE and SLAs

1. Monitor System Resources
![cpu](/images/cpu.png)
![memory](/images/memory.png)
![disk](/images/disk.png)

2. Disk Space Management

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
tmpfs             746192      2424    743768   1% /run
/dev/sda3      460269616 101144280 335671436  24% /
tmpfs            3730944     10572   3720372   1% /dev/shm
tmpfs               5120         4      5116   1% /run/lock
efivarfs             128        21       103  17% /sys/firmware/efi/efivars
tmpfs            3730944         0   3730944   0% /run/qemu
/dev/sda1         964900    192172    706376  22% /boot
/dev/nvme0n1p1     98304     51240     47064  53% /boot/efi
tmpfs             746188      1680    744508   1% /run/user/1000

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ sudo find /var -type f -exec du -h {} + | sort -n -r | head -n 3
1008K	/var/log/syslog.4.gz
1000K	/var/lib/docker/overlay2/61a6ac4fd7827b0f3d128c864abeaf4c7cfed126e35fa7926da32abacf3a23f0/diff/bin/arp
996K	/var/lib/docker/overlay2/1c58d899200e67086d4d4cca8e25e1c577c54b8bdfd04dea3735c6edd32a79c2/diff/usr/lib/x86_64-linux-gnu/libmvec.so.1
```
