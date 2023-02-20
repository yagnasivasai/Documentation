#Ceph

## On Cephadmin Node

sudo yum upgrade -y
sudo yum update -y
sudo yum install curl -y
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum update -y
sudo yum install -y python39
sudo yum install podman -y

hostnamectl set-hostname cephadmin
hostnamectl set-hostname cephnode1
hostnamectl set-hostname cephnode2

sudo tee -a /etc/hosts<<EOF
192.168.2.185    cephadmin
192.168.2.186    cephnode1
192.168.2.188    cephnode2
EOF

curl --silent --remote-name --location https://github.com/ceph/ceph/raw/quincy/src/cephadm/cephadm
chmod +x cephadm
./cephadm add-repo --release quincy
./cephadm install
which cephadm
cephadm bootstrap --mon-ip <ip>
cephadm shell
ceph orch host ls

ssh-copy-id -f -i /etc/ceph/ceph.pub root@192.168.2.186
ssh-copy-id -f -i /etc/ceph/ceph.pub root@192.168.2.188


sudo tee -a /etc/hosts<<EOF
172.31.89.114   ip-172-31-89-114.ec2.internal    
172.31.85.52    ip-172-31-85-52.ec2.internal
172.31.89.147   ip-172-31-89-147.ec2.internal
EOF

ceph orch host add ip-172-31-85-52.ec2.internal 172.31.85.52
ceph orch host add ip-172-31-89-147.ec2.internal 172.31.89.147

dnf install chrony -y
systemctl start chronyd
systemctl enable chronyd
systemctl status chronyd
vi /etc/chrony.conf
allow 192.168.56.0/24
systemctl restart chronyd
firewall-cmd --permanent --add-service=ntp
firewall-cmd --reload
https://www.tecmint.com/install-ntp-in-rhel-8/


useradd -d /home/ceph -m ceph
passwd ceph
visudo
ceph    ALL=(ALL)       NOPASSWD: ALL


ceph orch daemon add osd ceph-01:/dev/sdb
ceph orch daemon add osd ceph-02:/dev/sdb
ceph orch daemon add osd ceph-03:/dev/sdb
ceph orch daemon add osd ceph[0,1,2]:/dev/sd[b,c]
ceph orch daemon add osd ceph[0,1,2]:/dev/sd[b,c]


ceph orch device ls 
ceph osd tree
ceph tell mon.* injectargs --mon_allow_pool_delete true
ceph osd pool rm default.rgw.buckets.data default.rgw.buckets.data --yes-i-really-really-mean-it
python3 ceph.py \
--rbd-data-pool-name default.rgw.buckets.data
yum install python3-rbd -y
yum install python3-rados -y

![2023-01-24-10-28-42](https://user-images.githubusercontent.com/60940642/214216954-81f099f5-a49e-43c7-8a36-8d98841e31e1.png)
![2023-01-24-10-29-39](https://user-images.githubusercontent.com/60940642/214216958-66ef0a62-db66-4239-8339-f78222c44eb9.png)
![2023-01-24-10-43-00](https://user-images.githubusercontent.com/60940642/214216961-6a7610db-d698-4f53-91a0-686f7c2e4f47.png)

