# Log for XtratuM 3.7.3

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

> Error 1

```sh
fatal error: sys/types.h: No such file or directory
compilation terminated.
```

> Solution 1

```sh
sudo ln -s /usr/include/x86_64-linux-gnu/sys /usr/include/sys 
```
> Error 2

```sh
fatal error: bits/predefs.h: No such file or directory
compilation terminated.
```

> Solution 2

```sh
sudo apt-get install gcc-multilib
```

> Error 3

```sh
  - tools/xmcparser
/bin/sh: 1: xml2-config: not found
In file included from main.c:24:0:
parser.h:18:27: fatal error: libxml/parser.h: No such file or directory
compilation terminated.
```
> Error 4

```sh
# after installing libxslt1-dev_1.1.26-14.1_amd64.deb
  - tools/xmcparser
/usr/bin/ld: cannot find -lxml2
collect2: error: ld returned 1 exit status
```

> Solution 3 & 4

```sh
sudo dpkg--add-architecture i386
sudo apt-get update
sudo apt-get install libxml2-dev:i386
```
