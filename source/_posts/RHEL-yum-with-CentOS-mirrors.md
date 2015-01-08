---
title: 为RHEL配置Centos源
layout: post
tags: ['public', 'post', 'linux','RHEL', 'centos']
time: 2013-05-20 18:35
---

服务器的Redhat Enterprise Linux太旧了，最近为了装一些新的驱动程序，不得不升级系统。但是又没有注册到Redhat，而且年代已久，找不到如何注册了。

CentOS其实和RHEL的源代码是一样的。RHEL按照开源协议，需要公开源代码。CentOS就是开源社区自己编译了RHEL的源代码。因此CentOS的源可以配置给RHEL使用。

但是RHEL的yum默认是设置到了Redhat的更新服务器，需要进行一些配置。

以下步骤都是我在RHEL 6.3上的操作。在RHEL 6.x上应该是相同的操作，在RHEL 5.x的操作不完全一样，但是步骤应该类似。

1. 删除RHEL自带的yum。
``` nohls
rpm -aq | grep yum | xargs rpm -e --nodeps 
```
2. 安装CentOS的yum。下载以下的一些rpm包
``` nohls
python-iniparse-0.3.1-2.1.el6.noarch.rpm
yum-3.2.29-30.el6.centos.noarch.rpm
yum-metadata-parser-1.1.2-16.el6.x86_64.rpm
yum-plugin-fastestmirror-1.1.30-14.el6.noarch.rpm
```
安装rpm
``` nohls
rpm -Uvh *.rpm
```
3. 修改yum更新源。在/etc/yum.repos.d/目录下新建一个.repo文件，不妨命名为centos.repo。我使用了清华大学的更新源。
``` ini
[base]
name=CentOS-$releasever - Base
baseurl=http://mirrors.tuna.tsinghua.edu.cn/centos/6/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-6
#released updates
[updates]
name=CentOS-$releasever - Updates
baseurl=http://mirrors.tuna.tsinghua.edu.cn/centos/6/updates/$basearch/
gpgcheck=1
gpgkey=http://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-6
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
baseurl=http://mirrors.tuna.tsinghua.edu.cn/centos/6/extras/$basearch/
gpgcheck=1
gpgkey=http://mirrors.tuna.tsinghua.edu.cn/centos/RPM-GPG-KEY-CentOS-6
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
baseurl=http://mirrors.tuna.tsinghua.edu.cn/centos/6/centosplus/$basearch/
gpgcheck=1
enabled=0
```
4. 清除yum缓存。
``` nohls
yum clean all
```
5. 现在就可以happy地使用CentOS源更新RHEL了。最好更新一下本地已经下载的rpm。
``` nohls
yum update
```
