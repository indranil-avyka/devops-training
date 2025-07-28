# DAY 3

## Q10. Schedule a backup of /etc folder with 01 min frequency

**Command:**
```bash
touch /scripts/backup.sh
chmod a+x /scripts/backup.sh
vi /scripts/backup.sh
cat /scripts/backup.sh
crontab -u root -e
crontab -u root -l
cd /home/
ls -lth
```

**Output:**
```
root@LAPTOP-4LLMB98P:~# touch /scripts/backup.sh
root@LAPTOP-4LLMB98P:~# chmod a+x /scripts/backup.sh
root@LAPTOP-4LLMB98P:~# vi /scripts/backup.sh
root@LAPTOP-4LLMB98P:~# cat /scripts/backup.sh
#!/bin/bash
cp -r /etc /home/etc_backup_`date +%d-%b-%y:%H:%M:%s`
root@LAPTOP-4LLMB98P:~# crontab -u root -e
no crontab for root - using an empty one
crontab: installing new crontab
root@LAPTOP-4LLMB98P:~# crontab -u root -l
* * * ** /scripts/backup.sh
root@LAPTOP-4LLMB98P:~# cd /home/
root@LAPTOP-4LLMB98P:/home# ls -lth
total 12K
drwxr-xr-x 88 root     root     4.0K Jul 28 19:05 etc_backup_28-Jul-25:19:05:1753729502
drwxr-xr-x 88 root     root     4.0K Jul 28 19:04 etc_backup_28-Jul-25:19:04:1753729443
drwxr-x---  4 indranil indranil 4.0K Jul 28 18:22 indranil
```

## Q11. Schedule a task which shutdown machine at 09:30PM on second Saturday of every month

**Command:**
```bash
which poweroff
crontab -u root -e
crontab -u root -l
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# which poweroff
/usr/sbin/poweroff
root@LAPTOP-4LLMB98P:/# crontab -u root -e
no crontab for root - using an empty one
crontab: installing new crontab
root@LAPTOP-4LLMB98P:/# crontab -u root -l
30 21 8-14 * 06 /usr/sbin/poweroff
```

## Q11. Schedule a backup of /etc folder on last day of every month

**Command:**
```bash
vi /scripts/backup.sh
cat /scripts/backup.sh
crontab -u root -e
crontab -u root -l
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# vi /scripts/backup.sh 
root@LAPTOP-4LLMB98P:/# cat /scripts/backup.sh 
#!/bin/bash 
cp -r /etc /home/etc_monthly_backup_`date +%d-%b-%y:%H:%M:%s` 
root@LAPTOP-4LLMB98P:/# crontab -u root -e 
no crontab for root - using an empty one 
crontab: installing new crontab 
root@LAPTOP-4LLMB98P:/# crontab -u root -l 
59 23 28-31 * * [ "$(date +\%d -d tomorrow)" == "01" ] && /scripts/monthly_backup.sh
```

## Q12. Create a directory /oracle, all users can write and modify files created by other users, however only owner of file should be able to delete files

**Command:**
```bash
mkdir /oracle
chmod 1777 /oracle
ls -ld /oracle
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# mkdir /oracle
root@LAPTOP-4LLMB98P:/# chmod 1777 /oracle
root@LAPTOP-4LLMB98P:/# ls -ld /oracle
drwxrwxrwt 2 root root 4096 Jul 28 20:32 /oracle
```

## Q13. Create a script which will take full and incremental backup of /inorgdb folder to other system

**Command:**
```bash
mkdir /inorgdb
vi /scripts/backup_inorgdb.sh
cat /scripts/backup_inorgdb.sh
chmod a+x /scripts/backup_inorgdb.sh
/scripts/backup_inorgdb.sh
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# mkdir /inorgdb
mkdir: cannot create directory '/inorgdb': File exists
root@LAPTOP-4LLMB98P:/# vi /scripts/backup_inorgdb.sh
root@LAPTOP-4LLMB98P:/# cat /scripts/backup_inorgdb.sh
#!/bin/bash
rsync -a /inorgdb/ indranil@172.27.113.41:/home/indranil/inorgdb_`date +%d-%b-%y:%H:%M:%s`
echo "Backup done at $(date +%d-%b-%y:%H:%M:%S)"
root@LAPTOP-4LLMB98P:/# chmod a+x /scripts/backup_inorgdb.sh
root@LAPTOP-4LLMB98P:/# /scripts/backup_inorgdb.sh
indranil@172.27.113.41's password:
Backup done at 28-Jul-25:21:05:06
```

## Q14. Create a script which will add 100 users, list of users is stored in users file

**Command:**
```bash
touch /scripts/userss.txt
for i in $(seq 1 100); do echo "user$i" >> /scripts/userss.txt; done
vi /scripts/userss.txt
touch /scripts/users_add.sh
vi /scripts/users_add.sh
cat /scripts/users_add.sh
chmod a+x /scripts/users_add.sh
/scripts/users_add.sh
tail -3 /etc/passwd
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# touch /scripts/userss.txt
root@LAPTOP-4LLMB98P:/# for i in $(seq 1 100); do echo "user$i" >> /scripts/userss.txt; done
root@LAPTOP-4LLMB98P:/# vi /scripts/userss.txt
root@LAPTOP-4LLMB98P:/# touch /scripts/users_add.sh
root@LAPTOP-4LLMB98P:/# vi /scripts/users_add.sh
root@LAPTOP-4LLMB98P:/# cat /scripts/users_add.sh
#!/bin/bash
for i in `cat /scripts/userss.txt`
do
        useradd $i
done
echo "added 100 users"
root@LAPTOP-4LLMB98P:/# chmod a+x /scripts/users_add.sh
root@LAPTOP-4LLMB98P:/# /scripts/users_add.sh
added 100 users
root@LAPTOP-4LLMB98P:/# tail -3 /etc/passwd
user98:x:1098:1098::/home/user98:/bin/sh
user99:x:1099:1099::/home/user99:/bin/sh
user100:x:1100:1100::/home/user100:/bin/sh
```

## Q15. Create a script which will monitor disk utilization and share output of partitions which are consuming space more than 70%

**Command:**
```bash
touch /scripts/disk_alert.sh
chmod a+x /scripts/disk_alert.sh
vi /scripts/disk_alert.sh
cat /scripts/disk_alert.sh
/scripts/disk_alert.sh
df -h
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# touch /scripts/disk_alert.sh
root@LAPTOP-4LLMB98P:/# chmod a+x /scripts/disk_alert.sh
root@LAPTOP-4LLMB98P:/# vi /scripts/disk_alert.sh
root@LAPTOP-4LLMB98P:/# cat /scripts/disk_alert.sh
#!/bin/bash
echo "Partitions over 70% usage:"
df -hP | awk 'NR>1 && int($5) > 70 {print $0}'
root@LAPTOP-4LLMB98P:/# /scripts/disk_alert.sh
Partitions over 70% usage:
root@LAPTOP-4LLMB98P:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
none            1.9G     0  1.9G   0% /usr/lib/modules/6.6.87.2-microsoft-standard-WSL2
none            1.9G  4.0K  1.9G   1% /mnt/wsl
drivers         454G  280G  175G  62% /usr/lib/wsl/drivers
/dev/sdd       1007G  1.6G  955G   1% /
none            1.9G   96K  1.9G   1% /mnt/wslg
none            1.9G     0  1.9G   0% /usr/lib/wsl/lib
rootfs          1.9G  2.7M  1.9G   1% /init
none            1.9G  548K  1.9G   1% /run
none            1.9G     0  1.9G   0% /run/lock
none            1.9G     0  1.9G   0% /run/shm
none            1.9G   76K  1.9G   1% /mnt/wslg/versions.txt
none            1.9G   76K  1.9G   1% /mnt/wslg/doc
C:\             454G  280G  175G  62% /mnt/c
tmpfs           1.9G   16K  1.9G   1% /run/user/1000
tmpfs           379M   16K  379M   1% /run/user/0
```

## Q16. Create a partition of 1GB and mount it on /inorg-app1 directory

**Command:**
```bash
dd if=/dev/zero of=/partition.txt bs=1M count=1024
losetup /dev/loop10 /partition.txt
mkfs.ext4 /dev/loop10
mkdir -p /inorg-app1
mount /dev/loop10 /inorg-app1
df -h | grep inorg-app1
```

**Output:**
```
root@LAPTOP-4LLMB98P:/# dd if=/dev/zero of=/partition.txt bs=1M count=1024
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 1.54796 s, 694 MB/s
root@LAPTOP-4LLMB98P:/# losetup /dev/loop10 /partition.txt
root@LAPTOP-4LLMB98P:/# mkfs.ext4 /dev/loop10
mke2fs 1.47.0 (5-Feb-2023)
Discarding device blocks: done
Creating filesystem with 262144 4k blocks and 65536 inodes
Filesystem UUID: 607ea4c6-c7b7-46ba-97e7-e7c35cb46c30
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376
Allocating group tables: done
Writing inode tables: done
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done
root@LAPTOP-4LLMB98P:/# mkdir -p /inorg-app1
root@LAPTOP-4LLMB98P:/# mount /dev/loop10 /inorg-app1
root@LAPTOP-4LLMB98P:/# df -h | grep inorg-app1
/dev/loop10     974M   24K  907M   1% /inorg-app1
```