
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

在解决方案根目录下
```
git init
```

## 1.3 舍弃

项目有很多东西是多余的, 不要的, 那些都是编译过程中的中间文件/文件夹, 不是项目的核心文件, 包括:

* .vs文件夹及其下文件
* Debug文件夹及其下文件, 包括解决方案目录下的Debug和所有项目文件夹下的Debug
* x64文件夹及其下文件, 包括解决方案目录下的x64和所有项目文件夹下的x64
* .user文件

当使用git status检查仓库要commit的文件时会发现git会提示这些文件夹没有add, 然而这些文件夹是根本不应该add, 更不用说去commit的, 所以需要让git去忽略这些文件.

我们在根目录写一个`.gitignore`文件, 让git根据文件内容去忽略文件/文件夹. 根据我们上面列出来的要舍弃/忽略的文件夹, `.gitignore`的内容参考如下:

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

至此可以add文件到暂存区, 打`git status`检查仓库, 前面提到的要舍弃的文件应该不在待commit区里. 最后可以正式commit文件到仓库里.

# 1.4 同步

现在用`git status`检查仓库状态, 应该是