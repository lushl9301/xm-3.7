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
