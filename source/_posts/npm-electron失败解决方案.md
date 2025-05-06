---
title: npm electron失败解决方案
date: 2025-05-06 13:28:23
categories:
- 技术
tags:
- 前端
- electron
---
**项目中安装electron失败，通过修改electron仓库地址后，安装成功。**
1. 打开npm配置文件
```
npm config edit
```

2. 在空白处添加配置
```
registry=https://registry.npmmirror.com
electron_mirror=https://cdn.npmmirror.com/binaries/electron/
electron_builder_binaries_mirror=https://npmmirror.com/mirrors/electron-builder-binaries/
```

3. 保存后清除缓存，再次安装electron
```
npm cache clean --force
npm install electron -g
```