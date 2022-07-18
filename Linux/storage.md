
#### Check disk drives:
```bash
sudo fdisk -l
```
*Example:*
```bash
Device     Boot    Start      End  Sectors Size Id Type
/dev/vda1  *        2048 44037759 44035712  21G 83 Linux
/dev/vda2       44037760 52426367  8388608   4G 82 Linux swap / Solaris
```

#### Check Partitions 
*-h is used to show sizes in Megabytes, Gigabytes etc.*
```bash
sudo df -h
```
*Should look like this:*
```bash
Filesystem      Size  Used Avail Use% Mounted on
udev            967M     0  967M   0% /dev
tmpfs           199M  564K  199M   1% /run
/dev/vda1       4.4G  1.9G  2.4G  44% /
tmpfs           994M     0  994M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           994M     0  994M   0% /sys/fs/cgroup
tmpfs           199M     0  199M   0% /run/user/0
```

#### When /dev/(sda1/vda1 etc) are not the same size
*this (21G):*
```bash
Device     Boot    Start      End  Sectors Size Id Type
/dev/vda1  *        2048 44037759 44035712  21G 83 Linux
```
*and this are not matching (2.4G):*
```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1       4.4G  1.9G  2.4G  44% /
```
*run this:*
```bash
sudo resize2fs /dev/vda1
```
*check Paritions again:*
```bash
sudo df -h
```
*Should now look like this:*
```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        21G  1.9G   18G  10% /
```