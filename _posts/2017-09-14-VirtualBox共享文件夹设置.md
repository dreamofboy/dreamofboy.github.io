---
layout: post
title: VirtualBox共享文件夹设置
---

以前虚拟机设置共享文件夹是很直接很容易的。这次使用VirtualBox，遇到了一点小障碍。

Guest OS: Ubuntu 16.04 LTS
Host OS: Windows 10

按常规在VirtualBox的设置中，设置好共享文件夹 —— 只勾选自动加载。
启动虚拟机Ubuntu，试图进入共享文件夹，sf_xxx，提示没有权限。
于是，将当前用户加入vboxsf用户组：sudo adduser username vboxsf，尝试进入共享文件夹，尽管windows中已经在该文件夹放入了文件，但Ubuntu中看上去依然空空如也。

再次尝试Mount:
sudo mkdir /mnt/shared
sudo mount -t vboxsf share /mnt/shared
share就是创建的windows下共享文件夹的名字。

终于可以了。

----------
