# Virtualization

## KVM

### Convert VirtualBox Appliance to KVM Appliance

~~~ bash
# Unpack OVA
tar -xf vm-appliance.ova
# Convert disk from VDI to QCOW2
qemu-img convert -f vdi -O qcow2 vm-disk-name.vdi vm-disk-name.qcow2
~~~

### List Running VMs

~~~ bash
virsh list
~~~

### List VM Snapshots

~~~ bash
virsh snapshot-list --domain vm-name
~~~

### Create VM Snapshot

~~~ bash
virsh snapshot-create-as --domain vm-name --name "snapshot-name"
~~~

### Restore VM Snapshot

~~~ bash
virsh snapshot-revert --domain vm-name --snapshotname "snapshot-name"
~~~

### Delete VM Snapshot

~~~ bash
virsh snapshot-delete --domain vm-name --snapshotname "snapshot-name"
~~~
