#Deploy Upstream OpenStack in KVM machines:

##Assumptions:
1. This setup can be used for Deploying Upstream Openstack

##Provision KVM Servers:

###Create Management Network  10.0.0.1/24

```
virsh net-define management-net.xml
virsh net-start management-net
virsh net-autostart management-net
```

###Create External Network  203.0.113.1/24

```
virsh net-define external-net.xml
virsh net-start external-net
virsh net-autostart external-net
```

### Install Ubuntu 16.04 server:
```
sudo virt-install \
--name object1 \
--ram 2096 \
--disk path=/var/lib/libvirt/images/object1.qcow2,size=20 \
-c /home/archy/virtualbox/iso/ubuntu-16.04.1-server-amd64.iso \
--vcpus 2 \
--network network=os-vanila-management-net,model=virtio \
--video=vmvga --graphics vnc,listen=0.0.0.0
```

```
sudo virt-install \
--name object2 \
--ram 2096 \
--disk path=/var/lib/libvirt/images/object2.qcow2,size=20 \
-c /home/archy/virtualbox/iso/ubuntu-16.04.1-server-amd64.iso \
--vcpus 2 \
--network network=os-vanila-management-net,model=virtio \
--video=vmvga --graphics vnc,listen=0.0.0.0
```

