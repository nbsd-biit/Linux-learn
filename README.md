# Linux-learn
Learning Linux System/linux系统学习
## 第一章
### 1.1 ls命令
ls 【-a -l -h】 -a显示所有内容，包括隐藏文件，-l以列表形式展示更多细节，-h显示具体大小     
### 1.2 cd、pwd命令
cd 【文件路径】           
cd ..  #返回上一级          
cd #返回HOME目录            
pwd #查看当前工作目录     
### 1.3 mkdir命令
mkdir 【-p】【路径】【文件夹名】-p可选自动创建不存在的父级      
### 1.4 torch more cat 命令
touch 【路径】【文件】#创建文件       
cat 【路径】【文件】#查看文件内容      
more【路径】【文件】#用于查看多内容文件，用空格进行翻页，q退出    
### 1.5 cp mv命令
cp 【-r】【被复制的文件路径】【复制到的文件路径】，-r用于文件夹的复制   
mv 【被移动的文件路径】【移动到的文件路径】，-r用于文件夹的复制    
### 1.6 which find命令
which 【命令】#查找命令所在位置，例如：which pwd     
find 【起始路径】 -name "被查询的文件"     
find 【起始路径】 -size +|-n【KMG】  “|”表示或，+-表示大于或小于    
### 1.7 echo tail 重定向符
echo 类似print，echo 【输出内容】，也可以通过`（反引号）执行命令，例如；echo `ls -l`，反引号内当做命令执行      
重定向符>、>>，>为将左侧的命令结果覆盖到右侧指定文档中，>>为左侧的命令追加在右侧指定文件中     
tail为查看文件尾部信息，并可以持续跟踪，tail 【-f -num】【路径】【文件】，-f持续跟踪，-num查看倒数num个信息    
## 第三章
### 3.1 root用户
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
## Linux 系统安装git 
sudo apt update   
sudo apt install git -y   
git --version #检查是否安装成功，若出现版本号则成功   
git config --global user.name"【用户名】"   
git config --global user.email"【邮箱】"   
got config --list #查看配置   
## 第四章
### 4.1 常用快捷键
Ctrl+a 光标移动到开头      
Ctrl+e 光标移动到结尾    
Ctrl+左键 向左跳一个单词   
ctrl+右键 向右跳一个单词     
Ctrl+c 强制退出   
ctrl+d 退出或登出    
ctrl+r 搜索历史命令    
history 搜索历史命令  
ctrl+l 清屏     
### 4.2 软件安装
yum 【-y】【install |remove |search】【软件名】,-y自动确认，需要root权限和联网,centos    
apt 【-y】【install |remove |search】【软件名】,-y自动确认，需要root权限和联网，ubuntu     
### 4.3 systemctl控制软件
systemctl 【start|stop|status|enable|disable】【软件名】,分别为开始、结束、查看状态、开机自启、关闭开机自启    
### 4.4 软链接
ln -s 【被链接文件】【目的地】 类似快捷方式    
### 4.5 日期和时间
date 【-d】【格式化字符串】
### 4.6 ip和主机名
sudo apt install net-tools   
ifconfig 查看网络IP    
ping 【-c num】 ip或者主机名 -c为检查次数      
wegt 【-b】 url -b为后台下载      
curl 【-O】url 用于发送http网络请求，用于文件下载、获取信息，-O用于下载文件    
### 4.7 端口
nmap 【IP号】，查看IP对外暴漏的端口    
netstat -nap | grep 【端口号】，查看指定端口的占用    
### 4.8 进程
ps 【-e -f】-e显示所有进行，-f详细展示    
kill 【-9】 【进程ID】 -9为强制关闭进程    
### 主机状态监测
top 查看CPU、内存使用情况，-p显示某个进程信息，-d设置刷新时间，-c显示产生命令的详细指令，-n刷新次数，-i不显示闲置进程    
df 查看磁盘信息，-h更加详细
### 环境变量
echo$PATH 查看环境变量，PATH可替换    
export 【变量名】=【名字】，创建临时环境变量     
在HOME用户内通过 vi ~/.baserc export 【变量名】=【名字】source .baserc，只在当前用户生效    
增加全局环境变量在/etc/profile export 【变量名】=【名字】source /etc/profile，在全局生效    
### 解压压缩
Linux和Mac系统常用有2种压缩格式，后缀名分别是:   
①tar, 称之为tarball 归档文件,即简单的将文件组装到一个.tar的文件内,并没有太多文件体积的减少,仅仅是简单的封装   
②gz，也常见为tar.gz, gzip格式压缩文件,即使用gzip压缩算法将文件压缩到一个文件内，可以极大的减少压缩后的体积   
这两种格式使用tar命令均可以进行压缩和解压缩的操作语法:tar[-c -v-x-f-z-c] 参数1参数2 ... 参数N   
①-C,创建压缩文件，用于压缩模式   
②-V,显示压缩、解压过程，用于查看进度 -x,解压模式   
③-f,要创建的文件,或要解压的文件，-f选项必须在所有选项中位置处于最后一个 ④-z,gzip模式,不使用-z就是普通的tarball格式   
⑤-C,选择解压的目的地，用于解压模式   
tar的常用压缩组合为:   
①tar -cvf test.tar 1.txt 2.txt 3.txt   
将1.txt 2.txt 3.txt 压缩到test.tar文件内   
②tar -zcvf test.tar.gz 1.txt 2.txt 3.txt   
将1.txt 2.txt 3.txt 压缩到test.tar.gz文件内，使用gzip模式    
注意:-z选项如果使用的话，一般处于选项位第一个，-f选项，必须在选项位最后一个   
常用的tar解压组合有：   
①tar -xvf test.tar   
解压test.tar,将文件解压至当前目录   
②tar -xvftest.tar -C /home/itheima   
解压test.tar,将文件解压至指定目录(/home/itheima)   
③tar -zxvftest.tar.gz-C /home/itheima   
以Gzip模式解压test.tar.gz,将文件解压至指定目录(/home/itheima)   
注意: -f选项，必须在选项组合体的最后一位，-z选项，建议在开头位置，-C选项单独使用，和解压所需的其它参数分开   
zip 命令压缩文件：语法: zip [-r] 参数1参数2...参数N   
-r,被压缩的包含文件夹的时候，需要使用-r选项，和rm、cp等命令的-r效果一致   
zip test.zip a.txt b.txt c.txt
将a.txt b.txt c.txt 压缩到test.zip文件内
zip -r test.zip test itheima a.txt
将test、itheima两个文件夹和a.txt文件,压缩到test.zip文件内
unzip 命令解压文件：
语法: unzip [-d] 参数
-d,指定要解压去的位置,同tar的-C选项· 参数,被解压的zip压缩包文件
示例:
unzip test.zip,将test.zip解压到当前目录
unzip test.zip-d /home/itheima,将test.zip解压到指定文件夹内(/home/itheima)
# ROS2
VM虚拟机22.04，ros2 t
locale  # check for UTF-8   
sudo apt update && sudo apt install locales   
sudo locale-gen en_US en_US.UTF-8   
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8   
export LANG=en_US.UTF-8   
locale  # verify settings   
sudo apt update && sudo apt install curl -y
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')  
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-   source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"   
sudo dpkg -i /tmp/ros2-apt-source.deb    
sudo apt update   
sudo apt upgrade   
sudo apt install ros-humble-desktop  
