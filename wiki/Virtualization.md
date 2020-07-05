# Virtualization

## Convert VirtualBox Appliance to KVM Appliance

~~~ bash
qemu-img convert -f vdi -O qcow2 vm-disk-name.vdi vm-disk-name.qcow2
~~~
