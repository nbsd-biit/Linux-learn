# Linux-learn
Learning Linux System/linux系统学习
## 1.ls命令
## 2.
## 第三章
3.1root用户
linux 系统root权限（超级管理员），普通用户默认为在HOME目录内拥有所有权限，出了HOME目录只有执行和只读权限。
命令：su - 【用户名】 进入root权限，exit退出当前权限
sudo与su的区别在于，sudo的执行者为普通用户，只是临时获得root权限，普通用户要想获取root权限得通过配置root认证
获取权限认证方式：在root权限下输入 visudo ，在最后一行输入：【用户名】ALL=(ALL)      NOPASSWO: ALL,:WQ保存退出
3.2用户、用户组
不同用户和用户组有不同的权限，创建、删除用户组在root权限下
创建：groupadd 用户组名
删除：groupdel 用户组名
