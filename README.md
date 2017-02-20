#git优点：
分布式版本系统的最大好处之一
    是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，
    而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步。
    github有两种的上传方式：http 和密钥的形式

#windows下安装git
msysgit是Windows版的Git，从https://git-for-windows.github.io下载（网速慢的同学请移步国内镜像），然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，

当然也可以对某个仓库指定不同的用户名和Email地址



#linux下安装git
 root用户安装
```
$ yum install git  #提示输入y
```
输入git 查看git常用命令
```
$ git
```
安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "phpjimmy"
$ git config --global user.email "13783591763@163.com"
```

创建SSH Key：

```
$ ssh-keygen -t rsa -C "13783591763@163.com"
```

/root/.ssh/id_rsa  id_rsa.pub  known_hosts
```

$ cd root
$ ls -ah
$ cd .ssh
$ ls
$ vi id_rsa_pub
$ cp 
```

登录GitHub,点击右上角"Settings"，点击SSH and GPG keys,点击New SSH key,
填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”。


#创建版本库（版本库又名仓库，英文名repository）
初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：

    第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；

    第二步，使用命令git commit，完成。

git每次修改，如果不add到暂存区，那就不会加入到commit中


该仓库里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，

以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

第一步：选择一个合适的地方，创建一个空目录：
```
mkdir git_test
cd git_test
pwd
/d/wamp/apache2/htdocs/git/git_test
```
第二步：通过git init命令把这个目录变成Git可以管理的仓库
```
git init

```
修改 cat readme.txt 

添加 git add readme.txt
     git commit -m ""

查看状态 git status

撤销修改 git checkout -- readme.txt

把readme.txt文件在工作区的修改全部撤销，这里有两种情况:

  一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

  一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

git reset HEAD file 可以把暂存区的修改撤销掉（unstage），重新放回工作区

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。

删除文件 git rm readme.txt
        git commit -m ""

从版本库中删除文件 git rm readme.txt



#远程仓库
本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

第1步：创建SSH Key。在用户主目录下（C:\Users\Administrator\.ssh），看看有没有.ssh目录，

如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。

如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可

一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，

这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

点“Add Key”，你就应该看到已经添加的Key了。

GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

友情提示：在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

如果你不想让别人看到Git库，有两个办法：

一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。

另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。


#添加远程库
要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


第一步：登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

在Repository name填入仓库名git_test，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库。

根据GitHub的提示，让两个仓库进行远程同步（要关联一个远程库），在本地的git_test仓库下运行命令：
```
$ git remote add origin git@github.com:phpjimmy/git_test.git
```
第二步：就可以把本地库的所有内容推送到远程库上：
```
$ git push -u origin master
```
#把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，

还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

从现在起，只要本地作了提交，就可以通过命令：
```
$ git push origin master
```


#SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：
```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：
```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```
这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。



#从远程库克隆(要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆)
第一步：登陆GitHub，创建一个新的仓库，名字叫gitskills：

勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件：

第二步：用命令git clone克隆一个本地库：
      ```
       $ git clone git@github.com:phpjimmy/gitskills.git
       $ cd gitskills
       $ ls
       README.md
      ```

Git支持多种协议，包括https(https://github.com/phpjimmy/gitskills.git)，但通过ssh支持的原生git协议速度最快。


## 参考教程
[廖雪锋](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
重点参考教程中以下章节
[创建版本库](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)
[管理修改](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374829472990293f16b45df14f35b94b3e8a026220c5000)
[远程仓库](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)