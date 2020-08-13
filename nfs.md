**NFS Server**
[root@openswan-oel6 ~]# cd /nfs
[root@openswan-oel6 nfs]# vi a.txt
[root@openswan-oel6 nfs]# vi oci-oel.txt
[root@openswan-oel6 nfs]# vi aws-oci-vpn.txt

[root@openswan-oel6 ~]# yum install portmap nfs-utils* libgssapi
[root@openswan-oel6 ~]# vi /etc/exports
[root@openswan-oel6 ~]# cat /etc/exports
/nfs *(rw,sync)

[root@openswan-oel6 ~]# service iptables stop
iptables: Setting chains to policy ACCEPT: filter [ OK ]
iptables: Flushing firewall rules: [ OK ]
iptables: Unloading modules: [ OK ]

[root@openswan-oel6 ~]# /etc/init.d/rpcbind start
[root@openswan-oel6 ~]# /etc/init.d/rpcidmapd start
[root@openswan-oel6 ~]# /etc/init.d/nfs start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS mountd: [ OK ]
Starting NFS daemon: [ OK ]

[root@openswan-oel6 ~]#

**NFS Client**
[root@openswan ~]# yum install nfs-utils
[root@openswan ~]# mkdir -p /nfs_client

[root@openswan ~]# mount -t nfs 10.0.0.3:/nfs /nfs_client/
[root@openswan ~]# df -h
Filesystem Size Used Avail Use% Mounted on
devtmpfs 458M 0 458M 0% /dev
tmpfs 486M 0 486M 0% /dev/shm
tmpfs 486M 38M 449M 8% /run
tmpfs 486M 0 486M 0% /sys/fs/cgroup
/dev/sda3 39G 2.5G 36G 7% /
/dev/sda1 200M 9.7M 191M 5% /boot/efi
tmpfs 98M 0 98M 0% /run/user/0
tmpfs 98M 0 98M 0% /run/user/1000
10.0.0.3:/nfs 38G 2.0G 34G 6% /nfs_client
[root@openswan ~]# cd /nfs_client/
[root@openswan nfs_client]# ls
aws-oci-vpn.txt oci-oel.txt
