## 05.01_ftp：文件传输工具
- A、 vsftpd 
	- 一个开源免费的ftp服务器软件
	- 在Linux中最受推崇的FTP服务器，特点小巧轻快，安全易用	
- B、 xftp	
	- 一个开源免费的ftp客户端软件
- C、 安装服务器
	- sudo apt install vsftpd
- D、 启动服务器
	- systemctl start vsftpd 
	- service vsftpd start
- E、 停止服务器
	- systemctl stop vsftpd
	- service vsftpd   stop 
- F、 重启服务器
	- systemctl restart vsftpd 
	- service vsftpd restart 
- G、 上传和下载文件
	- 默认的ftp服务器端只支持下载，不支持上传，
	- 如果想要支持上传，需要设置配置文件/etc/vsftpd.conf
	- 更改配置文件
		- sudo vim /etc/vsftpd.conf	
		- write_enable=YES
		- 保存并退出
		- 注：配置文件中的语法格式 ： 属性=值    等号两边一定不能出现空格
- H、更改配置文件后，重启ftp服务器
	- systemctl restart vsftpd
	- service  vsftpd restart
- 参考资料：
	- https://blog.csdn.net/null_qiao/article/details/76919234
	- https://blog.csdn.net/lj402159806/article/details/78209103

## 05.02_Git概述
* A、 版本控制器,用处及好处
	- a. 便于开发,管理源码
	- b. 管理版本
	- c. 管理进度
* B、 使用场景
	- a. 除了新功能，更新版本
	- b. 项目挂掉了，还原版本
	- c. 甲方选择某个版本的代码
		- 第一天需要进度条  
		- 第二天对话框显示进度   
		- 第三天还是进度条好看 
	- d. 看程序员技术水平
	- e. 工作量统计---代码多,给的奖金多
	- f. 版本记录
* C、常见软件
	- a. svn (市场份额)    
	- b. git   
	- c. cvs   
	- d. vss (微软公司)  
	- e. ClearCase
* D、基本原理 
	- 1.客户端代码或文件提交到 服务器(仓库)
	- 2.客户端从服务器下载代码或文件
* E、提交代码的原则
	- 1. 先更新，再提交 
	- 2. 勤提交 
	- 3. 不要提交不能通过编译的代码 
	- 4. 每次提交必须书写明晰的标注 
	- 5. 提交时注意不要提交本地自动生成的文件 
	- 6. 不要提交自己不明白的代码 
          
* F、 Git和GitHub
	- git
		- Git 是一种专为处理文本文件而设计的版本控制系统。
		- 可以在你电脑不联网的情况下，只在本地使用的一个版本管理工具，
		- 可以让你更好的管理你的程序代码
	- github，
		- 是一个网站，就是每个程序员自己写的程序，可以在github上建立一个网上的仓库
		- 每次提交的时候可以把代码提交到网上，别人也都可以看到你的代码，同时别人也可以帮你修改你的代
		- 这种开源的方式非常方便程序员之间的交流和学习。
	- 总结
		- git可以认为是一个软件，能够帮你更好的写程序
		- github则是一个网站，这个网站可以帮助程序员之间互相交流和学习。
	- 参考资料：
		- https://blog.csdn.net/skyxmstar/article/details/65631658
		- https://blog.csdn.net/xiaoqiangyonghu/article/details/78400313


## 05.03_Git配置和使用
- github 配置 ---https://www.cnblogs.com/chengxs/p/6297659.html
- 1.安装git
	- sudo apt install git
- 2、配置git账号
	- git config --global user.name "git的用户名"
	- git config --global user.email "git的邮箱"
- 3、根据用户名及邮箱生成密钥(该密钥会用在该账号中)
	- 1. ssh-keygen -t rsa -C "git的邮箱"
	- 2. 执行后所有位置回车即可 
	- 3.生成的密钥默认存放在/home/用户名/.ssh 目录下
		- 密钥的文件为 id_rsa.pub
		- cat id_rsa.pub 可以查看密钥内容
		- 密钥范围为ssh至邮箱之前(不包含邮箱)
		- 复制该密钥。
- 4、网页端登陆github用户设置密钥
	- 将密钥复制到该用户的ssh密钥下
	- 用户 -> settings -> SSH&GPG keys -> new ssh key
- 5、检测密钥是否可用
	- ssh -T git@github.com
	- 见到Hi dushine2000! You've successfully authenticated ....代表成功
#####上传和下载用到的命令
	"""
	git init
	git add README.md
	git commit -m "first commit"
	git remote add origin https://github.com/dushine2000/HZ1806Project.git
	git push -u origin master
	"""


## 05.04_github上传及更新项目
- 1、需要在网页端创建一个新的仓库(项目)  new respository
- 2、当我们需要给新的项目respository上传内容时，使用init命令将我们需要上传的目录初始化
	- git init
	- 将一个普通文件初始化为可以链接git的文件
- 3、链接远程仓库
	- git remote add origin git项目地址
- 4、将需要上传到远程仓库的文件写在add后面
	- (该命令执行的路径为init过的文件路径下)
	- git add abc.txt
	- 让系统自动判断添加的文件：
	- git add .
- 5、将add后的文件提交到本地仓库
	- git commit -m "提交的信息"
- 6、将提交的内容同步至github上
	- git push -u origin master 
	- (如果正常可以提交文件，不要使用强制提及；如果正常提交失败，可以尝试强制提交)
	- 强制提交： git push -u origin +master
- 7.问题: 拒绝上传
	- 解决:修改配置文件
	- 1.进入当前共享文件的 .git 目录    cd .git
	- 2.编辑 config      vim config
	- 3.将url地址改成github中项目的 ssh地址
	- 4.保存并退出
	- 5.再次提交, 不需要输入账号密码

## 05.05_更新已经在github上存在的项目(自己电脑上没有该项目)
- 1、将github上的项目clone到本地某一路径下
	- git clone git项目地址
- 2、将需要上传到远程仓库的文件写在add后面
	- (该命令执行的路径为init过的文件路径下)
	- git add abc.txt
	- 让系统自动判断添加的文件：
	- git add .
- 3、将add后的文件提交到本地仓库
	- git commit -m "提交的信息"
- 4、将提交的内容同步至github上
	- git push -u origin master 
	- (如果正常可以提交文件，不要使用强制提及；如果正常提交失败，可以尝试强制提交)
	- 强制提交： git push -u origin +master


## 05.06_修改github的项目（前提：本地已经存在该项目，只是更新部分内容）
- 1、将需要上传到远程仓库的文件写在add后面
	- (该命令执行的路径为init过的文件路径下)
	- git add abc.txt
	- 让系统自动判断添加的文件：
	- git add .
- 2、将add后的文件提交到本地仓库
	- git commit -m "提交的信息"
- 3、将提交的内容同步至github上
	- git push -u origin master 
	- (如果正常可以提交文件，不要使用强制提及；如果正常提交失败，可以尝试强制提交)
	- 强制提交： git push -u origin +master

## 05.07_当多人合作开发时
- 1、更新本地仓库
	- git fetch origin
- 2、其他指令（提交等指令）与之前一致





## 05.08_安装nginx服务器
* Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，并在一个BSD-like 协议下发行。
* 其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好
* 中国大陆使用nginx网站用户有：百度、京东、新浪、网易、腾讯、淘宝等。
* 安装方法
	- 1.去nginx官网：	www.nginx.org
	- 2.右侧选择documentation--packages
	- 3.文档中找官网安装方式
	- 4.下载认证密钥
		- wget http://nginx.org/keys/nginx_signing.key
		- 会下载到当前目录下的nginx_signing.key文件中
	- 5.安装
		- sudo apt-key add nginx_signing.key
	- 6.配置源
		- 切换到对应的文件,并编辑
		- vim  /etc/apt/sources.list
		- 加上源:
		- deb http://nginx.org/packages/ubuntu/ codename nginx
		- deb-src http://nginx.org/packages/ubuntu/ codename nginx 
		- 注意将codename替换成当前codename  16.04 对应为: xenial
		- 保存退出
	- 7.更新跟安装
		- apt-get update
		- apt-get install nginx
	- 8.启动 sudo nginx
	- 9.查看nginx服务是否开启
		- ps -ef | grep nginx
	- 10.直接输入地址可以访问 即可.. 


* 参看资料01：http://nginx.org/en/linux_packages.html
* 参看资料02：https://blog.csdn.net/b_evan/article/details/72858149
 