---
title: 使用Linux搭建tModloader服务器
banner_img: /img/bg_image/too_any_losing_heroines/I_was_dumped.png
tags: 
    - 泰拉瑞亚
    - 游戏
    - Steam
    - 教程
categories: 
    - 游戏
---

# 环境
云服务商：京东云轻量级云服务器
系统：Ubuntu 22.04.3 LTS
CPU：双核
内存：4GB
宽带：5Mbps

# 步骤
## 1.安装Steamcmd
登陆你的Linux操作系统
在开始之前，必须先安装运行Steamcmd所需的依赖：

    sudo apt-get install lib32gcc1 //Bash

用于下载你需要的模组

    sudo apt install steamcmd //Bash

***其它系统安装请阅读Steamcmd的官网***

输入steamcmd，尝试运行steamcmd，成功后输入exit退出
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/steamcmd.png)

## 2.获取tModLoader
进入[tModLoader的releases](https://github.com/tModLoader/tModLoader/releases)
找到最新发布的文件，当前最新版本为v2024.10.3.0
复制tModLoader.zip的下载地址
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/tmodloader-ver.png)

在GitHub上下载tModLoader服务端
***如果你在中国大陆，那么连接Github需要科学上网，[在Linux上部署Clash](https://www.noseeflower.icu/)***

    wget https://github.com/tModLoader/tModLoader/releases/download/v2024.10.3.0/tModLoader.zip //Bash

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/wget.png)

    unzip tModLoader.zip //Bash

文件结构如下：

    ├── DedicatedServerUtils
    ├── dotnet
    ├── LaunchUtils
    ├── Libraries
    ├── RecentGitHubCommits.txt
    ├── start-tModLoader.bat
    ├── start-tModLoader-FamilyShare.bat
    ├── start-tModLoader-FamilyShare.sh
    ├── start-tModLoaderServer.bat
    ├── start-tModLoaderServer.sh
    ├── start-tModLoader.sh
    ├── steam_appid.txt
    ├── tMLMod.targets
    ├── tModLoader.deps.json
    ├── tModLoader.dll
    ├── tModLoader-Logs
    ├── tModLoader.pdb
    ├── tModLoader.runtimeconfig.dev.json
    ├── tModLoader.runtimeconfig.json
    ├── tModLoader.xml
    ├── tModPorter
    └── tModPorter.dll.config

进入tModLoader文件夹

    cd tModLoader //Bash

赋予start-tModLoaderServer.sh执行权限

    chmod u+x start-tModLoaderServer.sh //Bash

尝试第一次执行, 会自动安装需要的依赖dotnet

    ./start-tModLoaderServer.sh //Bash

输入n，不使用Steam的服务器

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/run.png)
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/zhumi.png)

Ctrl+c退出，下一步处理模组

## 3.下载&安装模组

启动tModLoader

# 参考链接
[Steamcmd官网](https://developer.valvesoftware.com/wiki/Zh/SteamCMD)
[tModLoader官方教程](https://github.com/tModLoader/tModLoader/wiki/Starting-a-modded-server)


























