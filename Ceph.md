#Ceph

+ https://balderscape.medium.com/setting-up-a-virtual-single-node-ceph-storage-cluster-d86d6a6c658e

## On Cephadmin Node

sudo yum upgrade -y

sudo yum update -y

sudo yum install curl -y

sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum update -y
sudo yum install -y python39
sudo yum install podman -y <<-Install on both master and worker->>

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
ceph orch daemon add osd ceph-01:/dev/sdb
ceph orch daemon add osd ceph-02:/dev/sdb
ceph orch daemon add osd ceph-03:/dev/sdb
ceph orch daemon add osd ip-172-31-6-11.ap-south-1.compute.internal:/dev/sdf
ceph orch daemon add osd ip-172-31-39-83.ap-south-1.compute.internal:/dev/sdg
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
![2023-01-24-10-28-42](https://user-images.githubusercontent.com/60940642/214216954-81f099f5-a49e-43c7-8a36-8d98841e31e1.png)
![2023-01-24-10-29-39](https://user-images.githubusercontent.com/60940642/214216958-66ef0a62-db66-4239-8339-f78222c44eb9.png)
![2023-01-24-10-43-00](https://user-images.githubusercontent.com/60940642/214216961-6a7610db-d698-4f53-91a0-686f7c2e4f47.png)



https://towardsdatascience.com/run-your-spark-data-processing-workloads-using-opendatahub-ocs-and-an-external-ceph-cluster-8922f166f884



[root@localhost ~]# curl -L -w %{url_effective} -o /dev/null -s https://github.com/ceph/ceph/raw/quincy/src/cephadm/cephadm
https://raw.githubusercontent.com/ceph/ceph/quincy/src/cephadm/cephadm[root@localhost ~]# 
[root@localhost ~]# sudo subscription-manager repos --enable=rhceph-5-tools-for-rhel-8-x86_64-rpms
Repository 'rhceph-5-tools-for-rhel-8-x86_64-rpms' is enabled for this system.




cephadm bootstrap --mon-ip 172.31.6.11 \
--allow-fqdn-hostname \
--single-host-defaults