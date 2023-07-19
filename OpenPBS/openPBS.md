# OpenPBS

### Step 1: install packages
```bash
# clone the openpbs repo
git clone https://github.com/openpbs/openpbs.git

# install deveopment tools
yum groupinstall "Development Tools"

```
![](./images/1.jpg)

### Step 2: install OpenPBS
```bash
# rename the folder the folder
mv ./openpbs/ ./openpbs-23.06.06

# create a tar file 
tar -cvf /root/rpmbuild/SOURCES/openpbs-23.06.06.tar.gz openpbs-23.06.06/ 

# navigate to the folder
cd openpbs-23.06.06/

# build the rpm file
rpmbuild -ba openpbs.spec

# to extract the dependencies list(Optional)
rpmbuild -ba openpbs.spec
cat dependencies_list | sed -n '4,20p' | awk '{print $1}'

# install the dependencies
yum install -y libtool-ltdl-devel hwloc-devel libX11-devel libXt-devel libedit-devel libical-devel ncurses-devel postgresql-devel postgresql-contrib python3-devel tcl-devel tk-devel zlib-devel expat-devel openssl-devel libXext libXft gcc hwloc-devel;

# navigate to the directory 
cd /root/rpmbuild/RPMS/x86_64 

# install opebpbs-server
yum install openbps-server-23.06

```
![](./images/2.jpg)

### Step 3: configure pbs.conf
```bash
# change ownership of the file 
chmod 4755 /opt/pbs/sbin/pbs_iff /opt/pbs/sbin/pbs_rcp

# to start the services
systemctl start pbs

# to check the status of the service
/etc/init.d/pbs status

# to source the environment
. /etc/profile.d/pbs.sh

```
![](./images/3.jpg)
![](./images/4.jpg)
![](./images/5.jpg)
![](./images/6.jpg)



















