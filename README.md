
# 1 上传项目到GitHub的简易说明

## 1.1 准备

**请务必不要让系统隐藏文件后缀名**,这是一个开启显示后缀名的教程:

[Win10文件扩展名(后缀名)怎么显示/隐藏](https://www.xiazaiba.com/jiaocheng/2636.html)

**请务必让系统显示隐藏文件夹**,`.vs`文件是隐藏文件夹, 文件夹隐藏开启时, 难以操作.vs文件夹.

一开始我们有一个HelloWorld项目, 目录结构如下:
```
│  HelloWorld.sln
│
├─Debug
│      HelloWorld.exe
│      HelloWorld.ilk
│      HelloWorld.pdb
│
├─HelloWorld
│  │  HelloWorld.vcxproj
│  │  HelloWorld.vcxproj.filters
│  │  HelloWorld.vcxproj.user
│  │  main.cpp
│  │
│  ├─Debug
│  │  │  HelloWorld.log
│  │  │  main.obj
│  │  │  vc141.idb
│  │  │  vc141.pdb
│  │  │
│  │  └─HelloWorld.tlog
│  │          CL.command.1.tlog
│  │          CL.read.1.tlog
│  │          CL.write.1.tlog
│  │          HelloWorld.lastbuildstate
│  │          link.command.1.tlog
│  │          link.read.1.tlog
│  │          link.write.1.tlog
│  │
│  └─x64
│      └─Debug
│          │  HelloWorld.log
│          │  main.obj
│          │  vc141.idb
│          │  vc141.pdb
│          │
│          └─HelloWorld.tlog
│                  CL.command.1.tlog
│                  CL.read.1.tlog
│                  CL.write.1.tlog
│                  HelloWorld.lastbuildstate
│                  link.command.1.tlog
│                  link.read.1.tlog
│                  link.write.1.tlog
│
└─x64
    └─Debug
            HelloWorld.exe
            HelloWorld.ilk
            HelloWorld.pdb
```

## 1.2 建立仓库

在github上建立一个新仓库, 然后使用仓库的地址clone到本地.

可以clone的地址类似这样
```
git@github.com:airaou/HelloWorld.git
```
或这样
```
https://github.com/airaou/HelloWorld.git
```

在本地准备好要放仓库文件夹的地方, 打
```
git clone <仓库地址>
```
来clone仓库到本地.

## 1.3 复制与舍弃

把整个解决方案复制到仓库文件夹下, .sln文件和.git文件夹处于同一个目录.

项目有很多东西是多余的, 不要的, 那些都是编译过程中的中间文件/文件夹, 不是项目的核心文件, 包括:

* .vs文件夹及其下文件
* Debug文件夹及其下文件, 包括解决方案目录下的Debug和所有项目文件夹下的Debug
* x64文件夹及其下文件, 包括解决方案目录下的x64和所有项目文件夹下的x64
* *.user文件

当使用`git status`检查仓库要commit的文件时会发现git会提示这些文件夹没有add, 然而这些文件夹是根本不应该add, 更不用说去commit的, 所以需要让git去忽略这些文件.

我们在仓库根目录写一个`.gitignore`文件, 让git根据文件内容去忽略文件/文件夹. 根据我们上面列出来的要舍弃/忽略的文件夹, `.gitignore`的内容参考如下:

```
.vs
Debug
x64
*.user
```

Windows下可能无法直接创建`.gitignore`文件, 可以在git bush里输入
```
echo > .gitignore
```
来创建`.gitignore`文件.

至此可以add文件到暂存区, 打`git status`检查仓库, 前面提到的要舍弃的文件应该不在待commit区里.

下面检查仓库的结果
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   .gitignore
        new file:   HelloWorld.sln
        new file:   HelloWorld/HelloWorld.vcxproj
        new file:   HelloWorld/HelloWorld.vcxproj.filters
        new file:   HelloWorld/main.cpp
        new file:   README.md
```
可以看到Debug, x64之类的文件夹下的文件全部都不在仓库管理范畴内.

最后可以正式commit文件到仓库里.

注意commit时附加的信息的中文最好使用utf-8编码, 使用gb2312编码的话, 在github上显示会乱码. git bush一般默认是使用utf-8编码的, 所以一般应该可以直接在git bush里使用中文.

最后可以添加个README.md文件, 让你的仓库在github有个简单的"首页".

# 1.4 同步

现在用`git status`检查仓库状态, 应该是干净的.

补充好个人信息后(只用配置一次, 本机生成id_rsa, 将公钥上传到github, 让你能用这台电脑的git同步仓库到github, 详见[远程仓库](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000))

即可push仓库到远端.