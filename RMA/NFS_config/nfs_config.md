# How to config NFS Server

```bash
Pre-requisites:
disable selinux
disable firewall
change hostname if required
```
![selinux](./images/1.jpg)
![selinux](./images/2.jpg)

### Step 1: first install the package
```bash
yum install -y nfs-utils
```
![selinux](./images/3.jpg)


### Step 2: start the service
```bash
systemctl start nfs-server rpcbind
systemctl enable nfs-server rpcbind
```
![selinux](./images/4.jpg)

### Step 3: select directory to host
```bash
chmod 777 /home/
```
![selinux](./images/5.jpg)

### Step 4: make entry of the shared file in the /etc/exports
```bash
/home 10.10.10.0/24(rw,sync,no_root_squash)
# dont give space between ip(permissions), this will lead to read only file system error
```
![selinux](./images/6.jpg)


### Step 5: export the shared directories using given command
```bash
exportfs -r
# exportfs -v : dispalys a list of shared file and export options on server
# exportfs -a : exports all directories listed in /etc/exports
# exportfs -u : unexport one or more directories
# exportfs -r : re-export all directories after modifying /etc/exports
```
![selinux](./images/7.jpg)


### Step 6: configure the firewall
```bash
firewall-cmd --permanent --add-service mountd
firewall-cmd --permanent --add-service rpc-bind
firewall-cmd --permanent --add-service nfs
firewall-cmd --reload
```
![selinux](./images/8.jpg)
---
---
# Configure the Clients
### Step 7: install package on client 
```bash
yum install -y nfs-utils            
```
![selinux](./images/9.jpg)

### Step 8: check if shared file or directory is visible or not
```bash
showmount -e 10.10.10.158
```
![selinux](./images/10.jpg)

### Step 9: mount the shared directory
```bash
mount -t nfs 10.10.10.158:/home /home
# to check if given directory is mounted or not
mount | grep nfs 
# to check if given directory is mounted or not
df -hT
```
![selinux](./images/11.jpg)


### Step 10: how to enable automount
```bash
echo 10.10.10.158:/home /home   nfs nosuid,rw,sync,hard,intr    0   0 >> vi /etc/fstab
```
### Step 10: how to unmount the shared directory
```bash
umount /mnt/sharedFolder
```
![selinux](./images/12.jpg)


