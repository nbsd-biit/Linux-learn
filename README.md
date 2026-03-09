# Linux-learn
Learning Linux System/linux系统学习
## 1.ls命令
## 2.
## 第三章
### 3.1root用户
linux系统有超级管理员和普通用户，超级管理员有root权限，普通用户默认为在HOME目录内拥有所有权限，出了HOME目录只有执行和只读权限。
命令：su - 【用户名】 进入root权限，exit退出当前权限
sudo与su的区别在于，sudo的执行者为普通用户，只是临时获得root权限，普通用户要想获取root权限得通过配置root认证
获取权限认证方式：在root权限下输入 visudo ，在最后一行输入：【用户名】ALL=(ALL)      NOPASSWO: ALL,:WQ保存退出
### 3.2用户、用户组
不同用户和用户组有不同的权限，创建、删除用户和用户组在root权限下
创建：groupadd 【用户组名】
删除：groupdel 【用户组名】
useradd 【-g -d】【用户名】 ，-g指定用户的组 -d指定用户的HOME路径
userdel 【-r】【用户名】 ，-r删除用户的HOME路径
id 【用户名】，查看用户所属组
usermod -aG 【用户组】 【用户名】，指定用户加入用户组
getent passwd,查看所有用户
getent group ,查看所有用户组
### 3.3权限控制信息
权限细节一共10槽，例如：dwxrw-rx--，第一个d为文件夹，之后每三个分别为用户所属权限，用户组所属权限，其它权限，第一个还可以是-为文件，l为软链接，后面出现-表示对应无权限  
r读 w写 x执行权限 
### 3.4chmod命令
chmod用于修改文件和文件夹权限，只有root用户或者所属用户可以修改，chmod 【-R】【权限】 【文件或文件夹】，-R（可选）为将同一文件夹内所有内容权限进行修改，例如：chmod u=wrx,g=w,o=wr hello.txt，权限也可用数字表示，r为4，w为2，x为1，6表示rw，例如：chmod 751 hello.txt
### 3.5chown命令
chown用于修改文件和文件夹的用户和用户组，只有root用户可以修改，chown 【-R】【用户】 【:】 【用户组】 【文件或文件夹】。
