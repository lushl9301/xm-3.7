# xm-3.7 linux


### XtratuM installation
```sg
sudo apt-get install build-essential
sudo apt-get install libncurses5-dev libxml2-dev libxml2-utils makeself xorriso

cp xmconfig.x86 xmconfig
make menuconfig
make distro-run
```


### Linux Kernel Source Code

```sh
git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git

cd linux-stable
git checkout v3.4.4
# use git log -p to check the last commit
cd ..
cp -r linux-stable linux-3.4.4
rm -rf linux-3.4.4/.git linux-3.4.4/.gitignore
# make a backup
cp -r linux-3.4.4 linux-3.4.4.b
```

### Applying Patch

```sh
cp path/to/linux-xm3-3.4.4.patch .
# you should have linux-3.4.4/ and linux-xm3-3.4.4.patch in the same directory
patch -p1 < linux-xm3-3.4.4.patch
mv linux-3.4.4 linux-xm3-3.4.4
```

### Linux SDK

> Error

Cannot find drivers/iox/Kconfig

> Solution

Just fake one

```sh
cd linux-xm-3.4.4
ls arch/x86/configs/
# several configuration files shown
cp arch/x86/configs/xm_vmware_defconfig arch/x86/configs/kontron_defconfig
make kontron_defconfig

make XTRATUM_PATH=/opt/xm-sdk/xm ARCH=x86 vmlinux modules
```

> Install Linux SDK

```sh
cd arch/x86/xm/usr/bin/ # in linux folder
chmod +x ./*
cd - # go back to linux folder
sudo make distro-run
cd arch/x86/xm/usr/
sudo ./linux-3.4.4-xm.run
```

> Build Linux Kernel into XtratuM

```
cd xm-examples/xm3-examples/vmware-example
make resident_sw.iso
```

> Run Image File

```
qemu -m 2046 -serial stdio -hda resident_sw.iso
```

> Error

```
XM Hypervisor (3.7 r3)
Detected 2598.384MHz processor.
>> HWClocks [TSC clock (2598384Khz)]
[CPU0] >> HwTimer [i8253 timer (1193Khz)]
1 Partition(s) created
P0 ("linux-partition":0:1) flags: [ SYSTEM FP ]:
    [0xa0000:0xa0000 - 0xfffff:0xfffff] flags: 0x10
    [0x1800000:0x1800000 - 0x217fffff:0x217fffff] flags: 0x0
    [0xc0000000:0xc0000000 - 0xefffffff:0xefffffff] flags: 0x12
[TRAP] PAGE_FAULT(0xe)
CPU state:
EIP: 0x139:[<0xfbf801ae>] ESP: 0x141:[<0xfbf6fe74>] EFLAGS: 0x286  
EAX: 0x0 EBX: 0x1e7d001 ECX: 0xfbf6fee4 EDX: 0x1e7d000
ESI: 0x1 EDI: 0x1e7d000 EBP: 0xfe1
CR2: 0x1e7d000
Partition PANIC [0xfc030004:id(0)]:
error emulating IRQ (14) bad vector (14)
CPU state:
EIP: 0x139:[<0xfbf801ae>] ESP: 0x141:[<0xfbf6fe74>] EFLAGS: 0x286  
EAX: 0x0 EBX: 0x1e7d001 ECX: 0xfbf6fee4 EDX: 0x1e7d000
ESI: 0x1 EDI: 0x1e7d000 EBP: 0xfe1
CR2: 0x1e7d000
[HM] 5339103:XM_HM_EV_INTERNAL_ERROR (0):PART(0)
ip: 0xfbf801ae flags: 0x286
[HM] XM_HM_AC_PARTITION_HALT(7) XM_HM_LOG_ENABLED
[HM] Partition 0 halted
```
