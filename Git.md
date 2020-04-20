## Git简介

**Git是一个开源的分布式版本控制系统,用于敏捷高效地处理任何或小或大的项目**

**Git是 Linus torvalds为了帮助管理 Linux内核开发而开发的一个开放源码的版本控制软件**

**Git与常用的版本控制工具CVS, Subversion等不同,它采用了分布式版本库的方式,不必服务器端软件支持**

## 安装及配置

**Git安装后需配置用户相关信息**

```shell
yum -y install git
git config --global user.name "list"						# 安装gi版本控制软件
git config --global user.email "list@ta.163.com"			# 设置用户信息,如用户名、emai1等
git config --global core.editor vim							# 设置默认编辑器为vim
git config --list											# 查看用户配置
cat /root/.gitconfig
```

## 工作区、暂存区和版本库

**工作区:就是你在电脑里能看到的目录**

**暂存区:英文叫 stage,或 Gindex。一般存放在"gjt目录下"下的 index文件( git/index)中,所以我们把暂存区有时也叫作索引( index)**

**版本库:工作区有一个隐藏目录gt,这个不算工作区,而是Git的版本库**

## 创建仓库

**Git使用 git init命令来初始化一个Git仓库,Git的很多命令都需要在Git的仓库中运行,所以 git init是使用Gⅰt的第一个命令**

```shell
mkdir name
git init name/
```

## 添加文件到暂存区

**添加指定文件**

```shell
echo 'print("hello world!")' > /root/name/hello.py
cd /root/name/
git add hello.py
git status					# 查看状态
```

**添加所有文件**

```shell
cp /etc/hosts ./
git status
git add .
git commit -m "add hosts"
```

## 确认至仓库

**提交之前务必先设置用户信息**

```shell
git commit -m "初始化仓库"
git status
```

**添加追踪文件并提交到版本库**

```shell
echo 'print("done..")' >> hello.py
git commit -am "向hello.py添加新行"
```

## 删除跟踪文件

**要从Gⅰt中移除某个文件,就必须要从已跟踪文件清单中移除,然后提交**

```shell
git ls-files				# 查看版本库中文件
git rm world.py
git commit -m '删除world.py'
```

```shell
rm -rf *					# 不会将隐藏的.git删掉
git status
git checkout -- *
ll
```

## 分支管理

**每个git项目的分支叫作master**

```shell
git branch					# 查看分支
```

**如果你负责项目的一个功能,可以在某一个提交节点创建分支。注意,在创建分支的时候masten分支应该是干净**

```shell
git branch mybr1
git branch
有*号的表示masten分支
```

**在master分支提交代码**

```shell
cp /etc/passwd ./
git add .
git commit -m "master-a1"
```

**切换分支**

```shell
git checkout mybr1
git branch
ll						# 没有passwd文件
```

**在mybr1分支编写程序**

```shell
echo 'qwaszx' > sql
git add .
git commit -m "add sql"
git status
```

```shell
git branch
git checkout master
git branch
ll						## 有passwd,没有sql文件
```

**合并分支**

```shell
git merge mybr1
Merge branch 'mybr1'

# 请输入一个提交信息以解释此合并的必要性，尤其是将一个更新后的上游分支
# 合并到主题分支。
#
# 以 '#' 开头的行将被忽略，而且空提交说明将会终止提交。
```

## 搭建本地gtab服务器

**导入中文版gitlab镜像**

```shell
unzip docker.zip
cd docker/docker_pkgs/
yum -y install *.rpm
systemctl restart docker
systemctl enable docker
cd ../images/
docker load < gitlab_zh.tar
docker images
```

**

```shell
vim /etc/ssh/sshd_config
Port 2222			# 17行
systemctl restart sshd
################################################
docker run -d -h gitlab --name gitlab \
-p 443:443 -p 22:22 -p 80:80 --restart always \
-v /srv/gitlab/config:/etc/gitlab -v \
/srv/gitlab/logs:/var/log/gitlab -v \
/srv/gitlab/data:/var/opt/gitlab gitlab_zh
################################################
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
#################################################
reboot
docker ps			# 直到显示(health)才能正常访问
docker logs gitlab	# 日志文件
```

## 初始化 gitlab服务器

**配置Gitlab**

1.访问http://127.0.0.1,第一次需要设置root密码

![1](C:\Users\Administrator\Desktop\Gitlab\图片\1.png)

![2](C:\Users\Administrator\Desktop\Gitlab\图片\2.png)

## 添加gtab项目

**1.创建群组 group**

**使用群组管理项目和人员是非常好的方式**

**2.创建项目 project**

**存储代码的地方,里面还包含问题列表、维基文档以及其他一些Gtab功能**

**3.创建成员 member**

**添加你的团队成员或其他人员到Gtab**

## 创建群组

**创建名为devops的group(组)**

![3](C:\Users\Administrator\Desktop\Gitlab\图片\3.png)

![4](C:\Users\Administrator\Desktop\Gitlab\图片\4.png)

![5](C:\Users\Administrator\Desktop\Gitlab\图片\5.png)

## 创建用户

![6](C:\Users\Administrator\Desktop\Gitlab\图片\6.png)

![7](C:\Users\Administrator\Desktop\Gitlab\图片\7.png)

![8](C:\Users\Administrator\Desktop\Gitlab\图片\8.png)

![9](C:\Users\Administrator\Desktop\Gitlab\图片\9.png)

![10](C:\Users\Administrator\Desktop\Gitlab\图片\10.png)

## 创建项目

**创建名为myproject的项目**

![11](C:\Users\Administrator\Desktop\Gitlab\图片\11.png)

![12](C:\Users\Administrator\Desktop\Gitlab\图片\12.png)

![13](C:\Users\Administrator\Desktop\Gitlab\图片\13.png)

![14](C:\Users\Administrator\Desktop\Gitlab\图片\14.png)

![15](C:\Users\Administrator\Desktop\Gitlab\图片\15.png)

##  用户管理

**配置新建用户可以免密推送代码**

**使用新创用户list**

![16](C:\Users\Administrator\Desktop\Gitlab\图片\16.png)

![17](C:\Users\Administrator\Desktop\Gitlab\图片\17.png)

```shell
ssh-keygen -t rsa -C "list@163.com" -b 4096
ll /root/.ssh/id_rsa.pub
cat /root/.ssh/id_rsa.pub
```

![18](C:\Users\Administrator\Desktop\Gitlab\图片\18.png)

![19](C:\Users\Administrator\Desktop\Gitlab\图片\19.png)

```shell

```

