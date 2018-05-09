---
title: Git常用命令与配置
date: 2018-04-25 15:03:22
tags:
  - Git
---


一，配置私钥

```
    git config --global user.name "user"    //设置名字
    git config --global user.email "user@qq.com"  //设置邮箱  
    ssh-keygen -t rsa -C  //三次回车即可生成 ssh key
    ssh-keygen  //不同平台可以使用这个 ssh key
    cat ~/.ssh/id_rsa.pub  //查看你的 public key
```

   
----------
二，在gitee，coding，github添加你的key和ssh

 - 添加方法大同小异 个人 -> 设置 -> SSH 公钥 输入标题，以及public key，确认即可。

----------


三，git和gitee项目关联

  提交仓库

```
git add . //提交所有 
git add ''  //提交单个
git commit -m "first"  //提交时候设置的版本号
git push //提交 git push origin master
git remote add origin +"仓库地址"
git remote -v //查询权限
git push --force origin master //替换当前
```

    

  提取仓库

    
```
git clone //第一次拉取代码
git pull // 拉取代码 
git fetch --all //下载远程的库
git reset --hard origin/master //强制与master覆盖
```

  分支

```
git branch ''    //新建分支
git checkout ''  //切换分支
git pull    //拉取分支到本地开发
git branch   //查看当前分支
git branch -D '' //删除分支
git add . && git commit -m 'cont' && git push  //切换到分支,再提交内容，
git checkout master && git merge origin/分支名 && git push 切换到主分支,再合并分支
```
    