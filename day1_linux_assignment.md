# DAY1

## Q1. Create vadapav Directory inside root directory

### a. Create 10 files using touch command

**Commands:**
```bash
root@ubuntu:~# mkdir vadapav
root@ubuntu:~# cd vadapav/
root@ubuntu:~/vadapav# touch file{1..10}.txt
root@ubuntu:~/vadapav# ls -l
```

**Output:**
```
total 0
-rw-r--r-- 1 root root 0 Jul 27 21:13 file10.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file1.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file2.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file3.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file4.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file5.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file6.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file7.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file8.txt
-rw-r--r-- 1 root root 0 Jul 27 21:13 file9.txt
```

### b. Assign 000 permissions to all files

**Commands:**
```bash
root@ubuntu:~/vadapav# chmod 000 file*.txt
root@ubuntu:~/vadapav# ls -l
```

**Output:**
```
total 0
---------- 1 root root 0 Jul 27 21:13 file10.txt
---------- 1 root root 0 Jul 27 21:13 file1.txt
---------- 1 root root 0 Jul 27 21:13 file2.txt
---------- 1 root root 0 Jul 27 21:13 file3.txt
---------- 1 root root 0 Jul 27 21:13 file4.txt
---------- 1 root root 0 Jul 27 21:13 file5.txt
---------- 1 root root 0 Jul 27 21:13 file6.txt
---------- 1 root root 0 Jul 27 21:13 file7.txt
---------- 1 root root 0 Jul 27 21:13 file8.txt
---------- 1 root root 0 Jul 27 21:13 file9.txt
```

### c. Change ownership to N1 user

**Commands:**
```bash
root@ubuntu:~/vadapav# useradd N1
root@ubuntu:~/vadapav# chown N1 file*.txt
root@ubuntu:~/vadapav# ls -l
```

**Output:**
```
total 0
---------- 1 N1 root 0 Jul 27 21:13 file10.txt
---------- 1 N1 root 0 Jul 27 21:13 file1.txt
---------- 1 N1 root 0 Jul 27 21:13 file2.txt
---------- 1 N1 root 0 Jul 27 21:13 file3.txt
---------- 1 N1 root 0 Jul 27 21:13 file4.txt
---------- 1 N1 root 0 Jul 27 21:13 file5.txt
---------- 1 N1 root 0 Jul 27 21:13 file6.txt
---------- 1 N1 root 0 Jul 27 21:13 file7.txt
---------- 1 N1 root 0 Jul 27 21:13 file8.txt
---------- 1 N1 root 0 Jul 27 21:13 file9.txt
```

### d. Change group ownership to IT

**Commands:**
```bash
root@ubuntu:~/vadapav# groupadd IT
root@ubuntu:~/vadapav# chgrp IT file*.txt
root@ubuntu:~/vadapav# ls -l
```

**Output:**
```
total 0
---------- 1 N1 IT 0 Jul 27 21:13 file10.txt
---------- 1 N1 IT 0 Jul 27 21:13 file1.txt
---------- 1 N1 IT 0 Jul 27 21:13 file2.txt
---------- 1 N1 IT 0 Jul 27 21:13 file3.txt
---------- 1 N1 IT 0 Jul 27 21:13 file4.txt
---------- 1 N1 IT 0 Jul 27 21:13 file5.txt
---------- 1 N1 IT 0 Jul 27 21:13 file6.txt
---------- 1 N1 IT 0 Jul 27 21:13 file7.txt
---------- 1 N1 IT 0 Jul 27 21:13 file8.txt
---------- 1 N1 IT 0 Jul 27 21:13 file9.txt
```

### e. Create Directory A

**Commands:**
```bash
root@ubuntu:/# mkdir A
```

### f. Change permission of Dir A to 777 and ownership to N2 user

**Commands:**
```bash
root@ubuntu:/# useradd N2
root@ubuntu:/# chmod 777 A
root@ubuntu:/# chown N2 A
root@ubuntu:/# ls -l
```

**Output:**
```
drwxrwxrwx   2 N2   root    40 Jul 27 21:26 A
```

### g. Create 10 files in A dir and change permission of all to 000 including parent directory

**Commands:**
```bash
root@ubuntu:/# cd A
root@ubuntu:/A# touch file{1..10}.txt
root@ubuntu:/A# chmod 000 file*.txt
root@ubuntu:/A# ls -l
```

**Output:**
```
total 0
---------- 1 root root 0 Jul 27 21:32 file10.txt
---------- 1 root root 0 Jul 27 21:32 file1.txt
---------- 1 root root 0 Jul 27 21:32 file2.txt
---------- 1 root root 0 Jul 27 21:32 file3.txt
---------- 1 root root 0 Jul 27 21:32 file4.txt
---------- 1 root root 0 Jul 27 21:32 file5.txt
---------- 1 root root 0 Jul 27 21:32 file6.txt
---------- 1 root root 0 Jul 27 21:32 file7.txt
---------- 1 root root 0 Jul 27 21:32 file8.txt
---------- 1 root root 0 Jul 27 21:32 file9.txt
```

**Commands:**
```bash
root@ubuntu:/A# cd ..
root@ubuntu:/# chmod 000 A
root@ubuntu:/# ls -l
```

**Output:**
```
d---------   2 N2   root   240 Jul 27 21:32 A
```

## Q2. Copy the file /etc/fstab to /var/tmp and configure permissions

**Commands:**
```bash
root@ubuntu:/# cp /etc/fstab /var/tmp/fstab
```

### 1. The file /var/tmp/fstab is owned by root

**Commands:**
```bash
root@ubuntu:/# chown root /var/tmp/fstab
```

### 2. It belongs to group IT

**Commands:**
```bash
root@ubuntu:/# chgrp IT /var/tmp/fstab
```

### 3. Executable by everyone

**Commands:**
```bash
root@ubuntu:/# chmod a+x /var/tmp/fstab
root@ubuntu:/# ls -l /var/tmp/fstab
```

**Output:**
```
-rwxr-xr-x 1 root IT 59 Jul 27 21:52 /var/tmp/fstab
```

### 4. Natasha is able to read and write

**Commands:**
```bash
root@ubuntu:/# useradd Natasha
root@ubuntu:/# setfacl -m u:Natasha:rw /var/tmp/fstab
root@ubuntu:/# ls -l /var/tmp/fstab
```

**Output:**
```
-rwxrwxr-x+ 1 root IT 59 Jul 27 21:52 /var/tmp/fstab
```

### 5. Harry has no permissions

**Commands:**
```bash
root@ubuntu:/# useradd -m harry
root@ubuntu:/# setfacl -m u:harry:0 /var/tmp/fstab
root@ubuntu:/# getfacl /var/tmp/fstab
```

**Output:**
```
# file: var/tmp/fstab
# owner: root
# group: IT
user::rwx
user:Natasha:rw-
user:harry:---
group::r-x
mask::rwx
other::r-x
```

### 6. Others have only read permissions

**Commands:**
```bash
root@ubuntu:/# chmod o=r /var/tmp/fstab
root@ubuntu:/# ls -l /var/tmp/fstab
```

**Output:**
```
-rwxrwxr--+ 1 root IT 59 Jul 27 21:52 /var/tmp/fstab
```

## Q3. Take backup of entire /etc folder to /home folder

**Commands:**
```bash
root@ubuntu:/# rsync -cavz /etc/ /home/etc_`date +%d-%m-%y:%H:%M:%S`
```

**Output:**
```
sending incremental file list
created directory /home/etc_27-07-25:22:27:26
./
.pwd.lock
.resolv.conf.systemd-resolved.bak
.
.
.
sent 2,353,584 bytes  received 38,102 bytes  4,783,372.00 bytes/sec
total size is 21,730,764  speedup is 9.09
```