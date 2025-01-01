---
title: 使用Linux搭建tModLoader服务器
banner_img: /img/bg_image/too_any_losing_heroines/run.png
tags: 
    - 泰拉瑞亚
    - tModLoader
    - 游戏
categories: 
    - 教程
date: 2024-01-01 20:25:49
---

# 环境
云服务商：京东云轻量级云服务器
系统：Ubuntu 22.04.3 LTS
CPU：双核
内存：4GB
宽带：5Mbps
终端：[Tabby](https://github.com/Eugeny/tabby)

# 步骤
## 1.安装Steamcmd
登陆你的Linux操作系统
在开始之前，必须先安装运行Steamcmd所需的依赖：

    sudo apt-get install lib32gcc1

用于下载你需要的模组

    sudo apt install steamcmd

***其它系统安装请阅读Steamcmd的官网***

输入steamcmd，尝试运行steamcmd，成功后输入exit退出
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/steamcmd.png)

## 2.从Github获取tModLoader
进入[tModLoader的releases](https://github.com/tModLoader/tModLoader/releases)
找到最新发布的文件，当前最新版本为v2024.10.3.0
复制tModLoader.zip的下载地址
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/tmodloader-ver.png)

在GitHub上下载tModLoader服务端
***如果你在中国大陆，那么连接Github需要使用科学上网，[在Linux上部署Clash。](https://www.noseeflower.icu/)***

    wget https://github.com/tModLoader/tModLoader/releases/download/v2024.10.3.0/tModLoader.zip

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/wget.png)

解压tModLoader.zip

    unzip tModLoader.zip

tModLoader文件夹结构如下：

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

    cd tModLoader

赋予start-tModLoaderServer.sh执行权限

    chmod u+x start-tModLoaderServer.sh

尝试第一次执行, 会自动安装需要的依赖dotnet

    ./start-tModLoaderServer.sh

输入n，不使用Steam的服务器

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/run.png)
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/zhumi.png)

Ctrl+c退出，下一步处理模组

## 3.下载&安装模组

进入tModLoader文件夹

    cd tModLoader

创建一个名为install-Workshop-Mods.sh的可执行文件，并且赋予它执行权限

    touch install-Workshop-Mods.sh && chmod u+x install-Workshop-Mods.sh

编辑这个创建的文件

    vim install-Workshop-Mods.sh

按i更改vim为插入模式，复制粘贴以下内容(可以的话请看一下注释内容)

    # 定义一个函数用于安装Workshop模组
    function install_workshop_mods {
        # 声明一个局部变量用于存储steamcmd的命令
        local steamcmd_command

        # 从当前目录下的install.txt文件中读取每一行内容并赋值给变量lines
        lines=$(cat install.txt)
        
        # 遍历当前目录下的install.txt文件中的每一行（每个模组ID）
        for line in $lines; do
            # 将当前模组ID追加到steamcmd_command命令中
            steamcmd_command="$steamcmd_command +workshop_download_item 1281930 $line"
        done

        # 使用eval执行生成的steamcmd命令
        # +force_install_dir 设置模组安装路径为 ~/tModLoader/
        # +login anonymous 使用匿名用户登录
        # +quit 退出steamcmd
        eval "steamcmd +force_install_dir ~/tModLoader/ +login anonymous $steamcmd_command +quit"

        # 输出完成信息
        echo "Done"
    }

    # 调用install_workshop_mods函数以安装模组
    install_workshop_mods

按下esc，再按下:，输入wq退出编辑

打开你的tModLoader，确保你启用并且加载你要游玩的模组后
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/tmodloader.png)
来到模组整合包
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/mod-integration-package.png)
将已启用的模组生成为新的整合包
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/mod-integration-package-2.png)
整合包名称随意，生成后打开模组整合包文件夹
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/mod-integration-package-3.png)
进入你的模组整合包的Mods文件夹
使用SFTP工具(我这里使用的是Tabby自带的SFTP上传工具)，将install.txt上传到云服务器的tModLoader目录中
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/mod-integration-package-4.png)

运行install-Workshop-Mods.sh下载模组

    ./install-Workshop-Mods.sh

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/install-workshop-mods.png)

显示Success. Downloaded item xxxxxxxxx则表示下载成功

到这一步，已经完成了搭建，只差追一步启动服务器

## 4.启动&保持后台运行

启动之前先执行命令开启tModLoader需要的默认7777端口

    ufw allow 7777

配合screen命令进行使用方便管理
    
    apt-get install screen

使用screen创建一个窗口执行start-tModLoaderServer.sh

    screen -S tModLoader ./start-tModLoaderServer.sh

输入n，不使用Steam的服务器

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/run.png)
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/zhumi.png)

输入m

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-1.png)

输入e(启用全部模组)回车，再输入r(重新加载模组并且回到主界面)

![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-2.png)

输入n回车，创建新世界
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-3.png)

选择世界大小，输入的对应编号回车，1为小世界，2为中世界，3为大世界
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-4.png)

选择难度模式，输入的对应编号回车，1为经典，2为专家，3为大师，4为旅行
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-5.png)

选择世界感染，输入的对应编号回车，1为随机，2为孵化，3为血腥
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-6.png)

输入世界名称回车
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-7.png)

输入世界种子，默认回车就是随机种子
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-8.png)

生成世界ing
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-9.png)

输入对应的世界编号回车
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-10.png)

输入可容纳的玩家数量，默认16回车
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-11.png)

选择端口，默认7777回车(启动之前已经处理过了)
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-12.png)

选择是否转发端口，随意你是否开启
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-13.png)

输入服务器密码，默认不输入就是没有密码
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-14.png)

加载世界ing
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/start-server-15.png)

按下Ctrl+A+D退出当前窗口，使tModLoader在后台运行。 **(虽然它本来就会在后台运行，方便管理)**

需要再切换回tModLoader的界面使用

    screen -r tModLoader

***到此你已经完成了tModLoader服务器的搭建***

已经可以打开你的tModLoader，
多人游戏-通过IP加入-选择玩家-输入服务器IP地址-输入端口-输入密码(如果有的话)加入服务器开始游玩了。

# 废话
使用下方tModLoader官方教程搭建会更加方便，但是如果你要游玩Star Above模组，那我不建议使用官方的教程，因为未知原因导致你无法进入子世界，
所以我更建议使用这个方法。:D

# 参考链接
[Steamcmd官网](https://developer.valvesoftware.com/wiki/Zh/SteamCMD)
[tModLoader官方教程](https://github.com/tModLoader/tModLoader/wiki/Starting-a-modded-server)
