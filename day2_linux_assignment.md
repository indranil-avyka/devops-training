# DAY2

## Q3. Create a cascaded folder 1/2/3/4/5/6/7/8/9, create 100 files in folder 9, Archive and compress the same and copy to other system in /inorg-data folder

**Commands:**
```bash
root@ubuntu:~# mkdir -p 1/2/3/4/5/6/7/8/9
root@ubuntu:~# cd 1/2/3/4/5/6/7/8/9
root@ubuntu:~/1/2/3/4/5/6/7/8/9# touch {1..100}.txt
root@ubuntu:~/1/2/3/4/5/6/7/8/9# ls
```

**Output:**
```
100.txt  14.txt  19.txt  23.txt  28.txt  32.txt  37.txt  41.txt  46.txt  50.txt  55.txt  5.txt   64.txt  69.txt  73.txt  78.txt  82.txt  87.txt  91.txt  96.txt
10.txt   15.txt  1.txt   24.txt  29.txt  33.txt  38.txt  42.txt  47.txt  51.txt  56.txt  60.txt  65.txt  6.txt   74.txt  79.txt  83.txt  88.txt  92.txt  97.txt
11.txt   16.txt  20.txt  25.txt  2.txt   34.txt  39.txt  43.txt  48.txt  52.txt  57.txt  61.txt  66.txt  70.txt  75.txt  7.txt   84.txt  89.txt  93.txt  98.txt
12.txt   17.txt  21.txt  26.txt  30.txt  35.txt  3.txt   44.txt  49.txt  53.txt  58.txt  62.txt  67.txt  71.txt  76.txt  80.txt  85.txt  8.txt   94.txt  99.txt
13.txt   18.txt  22.txt  27.txt  31.txt  36.txt  40.txt  45.txt  4.txt   54.txt  59.txt  63.txt  68.txt  72.txt  77.txt  81.txt  86.txt  90.txt  95.txt  9.txt
```

**Commands:**
```bash
root@ubuntu:~/1/2/3/4/5/6/7/8/9# cd -
root@ubuntu:~# tar -cvf compressed.tar 1
root@ubuntu:~# ls -lh compressed.tar
```

**Output:**
```
-rw-r--r-- 1 root root 60K Jul 27 23:29 compressed.tar
```

**Commands:**
```bash
root@ubuntu:~# gzip compressed.tar
root@ubuntu:~# ls -lh compressed.tar.gz
```

**Output:**
```
-rw-r--r-- 1 root root 1.1K Jul 27 23:29 compressed.tar.gz
```

**Commands:**
```bash
root@ubuntu:~# ssh indranil@192.168.1.10
indranil@ubuntu:~$ sudo mkdir -p /inorg-data
indranil@ubuntu:~$ sudo chown indranil:indranil /inorg-data
indranil@ubuntu:~$ sudo -i
root@ubuntu:~# rsync -avz compressed.tar.gz indranil@192.168.1.10:/inorg-data/
```

**Output:**
```
indranil@192.168.1.10's password: 
sending incremental file list
compressed.tar.gz
sent 835 bytes  received 35 bytes  158.18 bytes/sec
total size is 1,053  speedup is 1.21
```

### Shell Script for File Transfer

**Script: transfer.sh**
```bash
#!/bin/bash
read -p "Enter file or folder name: " name
tar -cvf compressed.tar "$name"
gzip -f compressed.tar
rsync -avz compressed.tar.gz indranil@192.168.1.10:/inorg-data/
```

**Commands:**
```bash
root@ubuntu:~# nano transfer.sh
root@ubuntu:~# chmod +x transfer.sh
root@ubuntu:~# ./transfer.sh
```

**Output:**
```
Enter file or folder name: 1
1/
1/2/
1/2/3/
...
1/2/3/4/5/6/7/8/9/100.txt
indranil@192.168.1.10's password: 
sending incremental file list
compressed.tar.gz
sent 711 bytes  received 47 bytes  79.79 bytes/sec
total size is 1,053  speedup is 1.39
```

## Q4. Find out (Hardware Scanning)

### 1. Cores
**Commands:**
```bash
root@ubuntu:~# nproc
```

### 2. Memory
**Commands:**
```bash
root@ubuntu:~# free -h
```

### 3. Swap
**Commands:**
```bash
root@ubuntu:~# free -h
```

### 4. NIC info
**Commands:**
```bash
root@ubuntu:~# ip addr show
```

### 5. Disk info
**Commands:**
```bash
root@ubuntu:~# lsblk
```

### 6. Motherboard info
**Commands:**
```bash
root@ubuntu:~# dmidecode 2
```

### 7. Processor speed and make
**Commands:**
```bash
root@ubuntu:~# lscpu
```

### 8. PCI devices
**Commands:**
```bash
root@ubuntu:~# lspci
```

## Q5. Find out files named as passwd from entire system

**Commands:**
```bash
root@ubuntu:~# find / -type f -name passwd
```

**Output:**
```
/etc/pam.d/passwd
/etc/passwd
```

## Q6. Find out files whose size is exactly 100M

**Commands:**
```bash
root@ubuntu:~# find / -type f -size 100M
```

**Output:**
```
find: '/proc/18706/task/18706/net': Invalid argument
find: '/proc/18706/net': Invalid argument
find: '/proc/32088/task/32088/fdinfo/6': No such file or directory
find: '/proc/32088/fdinfo/5': No such file or directory
find: '/run/user/1002/doc': Permission denied
find: '/run/user/1002/gvfs': Permission denied
```

## Q7. Find out files whose size is between 100M to 1000M from entire system

**Commands:**
```bash
root@ubuntu:~# find / -type f -size +100M -size -1000M
```

**Output:**
```
find: '/proc/18706/task/18706/net': Invalid argument
find: '/proc/18706/net': Invalid argument
find: '/proc/32126/task/32126/fdinfo/6': No such file or directory
find: '/proc/32126/fdinfo/5': No such file or directory
find: '/run/user/1002/doc': Permission denied
find: '/run/user/1002/gvfs': Permission denied
/snap/firefox/5751/usr/lib/firefox/libxul.so
/snap/gnome-42-2204/202/usr/lib/x86_64-linux-gnu/libLLVM-15.so.1
/snap/ubuntu-desktop-bootstrap/315/usr/lib/x86_64-linux-gnu/libLLVM-15.so.1
/snap/thunderbird/644/usr/lib/thunderbird/libxul.so
/sys/devices/pci0000:00/0000:00:02.0/resource2_wc
/sys/devices/pci0000:00/0000:00:02.0/resource2
```

## Q8. Please allow N1 user only to read and access /inorg directory

**Commands:**
```bash
root@ubuntu:~# mkdir /inorg
root@ubuntu:~# chown N1 /inorg
root@ubuntu:~# chmod 500 /inorg
root@ubuntu:~# ls -ld /inorg
```

**Output:**
```
dr-x------ 2 N1 N1 40 Jul 28 00:28 /inorg
```

## Q9. Please allow IT group only to read and access /inorg directory

**Commands:**
```bash
root@ubuntu:~# chown :IT /inorg
root@ubuntu:~# chmod 050 /inorg
root@ubuntu:~# ls -ld /inorg
```

**Output:**
```
d---r-x--- 2 N1 IT 40 Jul 28 00:28 /inorg
```