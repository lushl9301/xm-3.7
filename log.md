# Log for XtratuM 3.7.3

## Must use Debian 7.8 i386 (Most Suitable Release)

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

### Compile XtratuM

> ALL OK


### Linux SDK

> Error

Cannot find drivers/iox/Kconfig

> Solution

NO
Just fake one

--------------------

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

# cd back to linux source code folder
sudo make distro-run
cd arch/x86/xm/usr/
sudo ./linux-3.4.4-xm.run
```

### Compile Examples

ERROR

Sometimes cannot fine xm-sdk-x86-xxx

> Solution

Just run XtratuM SDK installer to make a new sdk with the same name (easy way)
