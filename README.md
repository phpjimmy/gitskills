# gitskills

# git 基本使用

## 本地仓库
创建目录,在目录中初始化git仓库
命令
```
git init
// 通过编辑工具添加文件
git add *
git commit -m "init"
```

## 远程仓库
登录github等托管平台,新建仓库 -> new repo

## 本地仓库推送到服务器端
首次推送到服务器端,需要先把本地仓库与服务器端仓库关联
`git remote add origin git@github.com:your_user_name/your_repo_name.git`

以后使用只需要推送修改到服务器端
master 是分支名称, 其中 master 是默认的主分支名称
```
git push -u origin master
```

## 本地代码修改与同步
首次提交到远程仓库之后,通过工具修改文本或文件,
然后执行 仓库修改和推送命令

添加
```
// 添加指定的
git add filename
// 添加所有
git add *
```

修改
```
git add *
git commit -m ""
```

把修改同步到服务器命令
```
git push -u origin master
```

## 克隆命令
`git clone git@github.com:billoway/git_sz.git`

## 参考教程
[廖雪锋](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
重点参考教程中以下章节
[创建版本库](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)
[管理修改](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374829472990293f16b45df14f35b94b3e8a026220c5000)
[远程仓库](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)
