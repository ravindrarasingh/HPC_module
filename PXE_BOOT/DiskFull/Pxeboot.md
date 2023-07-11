# What is PXE?

```
Preboot execution environment(PXE), it is a method to boot other systems over the network, without any disk

packages required to configure the PXE bootserver

syslinux: this is bootloader which is used to boot the computenode by master    
    # we copy three file from syslinux package
    # 1. initrd.img 
    # 2. vmlinuz
    # copied from syslinux
    # 3. menu.c32
    # 4. pxelinux.0

dhcp: this package will be used to give ip to node which will be booting on the PXE boot network.

tftp-server: this package will be used to setup the TFTP server, which will be used tranfer the kernel to the node.

xinetd: xinetd (Extended Internet Service Daemon) is an open-source super-server daemon which runs on many Unix-like systems, and manages Internet-based connectivity.

httpd: this package will be used to host the pxeboot config

```

---
## How to configure PXE Boot server:

```
Pre-requisits for PXE_boot:

-> create new Vm's with two network adapters
    1. NAT : For Public network access
    2. Host-Only : For private network access
```


### Step 1 : setup the OS
---
* Disable the selinux  
`setenforce 0;`  
`sed -i 's/^SELINUX=.*$/SELINUX=disabled/g' /etc/selinux/config;`

* Disable the firewall  
`systemctl stop firewalld;`  
`systemctl disable firewalld;`

---
### Step 2 : Download the required packages
---
* Download the packages  
`yum install syslinux tftp-server httpd xinetd dhcp -y;`  
``