---
title: hexo-图片引入
date: 2018-04-25 15:03:22
tags:
  - hexo
---

-  根目录配置文件_config.yml

```
 post_asset_folder: true
```

 
- 安装一个可以上传本地图片的插件

```
npm install hexo-asset-image --save
```

- 添加图片，new create会自动创建文件夹存放图片
  + 新建一个文件
 + hexo new aaa
 + 新建文件aaa.md的同时也会创建aaa文件
 + 图片放入aaa文件夹里面
 + 图片引用代码如：

```
![logo](aaa/图片名字.png)
```