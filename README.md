# XMRig
fork https://github.com/xmrig/xmrig

# 编译
https://xmrig.com/docs/miner/build

# Centos7升级gcc（centos-release-scl方式）

## 安装scl源
```bash
yum install centos-release-scl scl-utils-build -y
```

## 列出scl有哪些源可以用
```bash
# yum list all --enablerepo='centos-sclo-rh'
# 由于结果太多，添加了grep过滤条件
yum list all --enablerepo='centos-sclo-rh' | grep devtoolset
```
```bash
# 结果已经删除其它版本，此处使用最新版本，目前最新是10。
devtoolset-10-gcc.x86_64                   10.2.1-2.1.el7         centos-sclo-rh
devtoolset-10-gcc-c++.x86_64               10.2.1-2.1.el7         centos-sclo-rh
devtoolset-10-gcc-gdb-plugin.x86_64        10.2.1-2.1.el7         centos-sclo-rh
devtoolset-10-gcc-gfortran.x86_64          10.2.1-2.1.el7         centos-sclo-rh
devtoolset-10-gcc-plugin-devel.x86_64      10.2.1-2.1.el7         centos-sclo-rh
devtoolset-10-gdb.x86_64                   9.2-9.sc1.el7          centos-sclo-rh
devtoolset-10-gdb-doc.noarch               9.2-9.sc1.el7          centos-sclo-rh
devtoolset-10-gdb-gdbserver.x86_64         9.2-9.sc1.el7          centos-sclo-rh
```

## 安装指定版本的devtoolset
```bash
yum install -y devtoolset-10-gcc.x86_64 devtoolset-10-gcc-c++.x86_64 devtoolset-10-gcc-gdb-plugin.x86_64
```
## 查看从 SCL 中安装的包的列表：
```bash
scl --list 或 scl -l

[root@centos7-build ~]# scl --list
devtoolset-10
```
## 激活对应的devtoolset
```bash
scl enable devtoolset-10 bash
```
## 查看版本
```bash
gcc -v
```
## 切换gcc版本
```bash
source ./enable

source /opt/rh/devtoolset-10/enable
```

## 直接替换旧的gcc
```
# 备份之前的gcc，如果之前并没有安装gcc，则不需要执行mv操作。
mv /usr/bin/gcc /usr/bin/gcc-4.8.5
mv /usr/bin/g++ /usr/bin/g++-4.8.5


ln -s /opt/rh/devtoolset-10/root/bin/gcc /usr/bin/gcc
ln -s /opt/rh/devtoolset-10/root/bin/g++ /usr/bin/g++

gcc --version
g++ --version

```
