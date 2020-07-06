# Virtualization

## Convert VirtualBox Appliance to KVM Appliance

~~~ bash
# Unpack OVA
tar -xf vm-appliance.ova
# Convert disk from VDI to QCOW2
qemu-img convert -f vdi -O qcow2 vm-disk-name.vdi vm-disk-name.qcow2
~~~
