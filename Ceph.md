#Ceph

sudo yum upgrade -y
sudo yum update -y
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum update -y
sudo yum install -y python39
sudo yum install -y yum-utils
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

ceph orch host add ip-172-31-85-52.ec2.internal 172.31.85.52
ceph orch host add ip-172-31-89-147.ec2.internal 172.31.89.147



sudo tee -a /etc/hosts<<EOF
172.31.89.114   ip-172-31-89-114.ec2.internal    
172.31.85.52    ip-172-31-85-52.ec2.internal
172.31.89.147   ip-172-31-89-147.ec2.internal
EOF

ssh-copy-id -f -i /etc/ceph/ceph.pub root@192.168.2.186
ssh-copy-id -f -i /etc/ceph/ceph.pub root@192.168.2.188

ceph orch host add ip-172-31-85-52.ec2.internal 172.31.85.52
ceph orch host add ip-172-31-89-147.ec2.internal 172.31.89.147

Optional

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/rhel/docker-ce.repo
    
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo yum install docker-ce
sudo systemctl enable --now docker
systemctl is-active docker
systemctl is-enabled docker
curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o docker-compose
sudo mv docker-compose /usr/local/bin && sudo chmod +x /usr/local/bin/docker-compose
sudo groupadd docker
sudo usermod -aG docker $USER
sudo systemctl enable docker.service
sudo systemctl enable containerd.service

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


sudo tee -a /etc/hosts<<EOF
192.168.1.231  ceph-01  ceph-01.localdomain
192.168.1.232  ceph-02  ceph-02.localdomain
192.168.1.233  ceph-03  ceph-03.localdomain
EOF


useradd -d /home/ceph -m ceph
passwd ceph
visudo
ceph    ALL=(ALL)       NOPASSWD: ALL


sudo tee -a /etc/hosts<<EOF
192.168.2.185    ceph-01
192.168.2.186    ceph-02
192.168.2.188    ceph-03
EOF

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



RADOS --- Reliable autonomic distributed object storage
![](2023-01-24-10-29-39.png)

It is a common layer for all types of storage (Block,Object,File)
![](2023-01-24-10-28-42.png)


![2023-01-24-10-28-42](https://user-images.githubusercontent.com/60940642/214216954-81f099f5-a49e-43c7-8a36-8d98841e31e1.png)
![2023-01-24-10-29-39](https://user-images.githubusercontent.com/60940642/214216958-66ef0a62-db66-4239-8339-f78222c44eb9.png)
![2023-01-24-10-43-00](https://user-images.githubusercontent.com/60940642/214216961-6a7610db-d698-4f53-91a0-686f7c2e4f47.png)

