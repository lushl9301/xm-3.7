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
cd arch/x86/xm/usr/bin/
chmod +x ./*
cd ..
sudo make distro-run
cd arch/x86/xm/usr/
sudo ./linux-3.4.4-xm.run
```
