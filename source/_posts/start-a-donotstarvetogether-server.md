---
title: 使用Linux搭建饥荒联机版服务器
banner_img: /img/bg_image/too_any_losing_heroines/I_was_dumped.png
tags: 
    - 饥荒联机版
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
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-tModloader-server/steamcmd.png)

## 2.获取饥荒联机版服务端
创建一个名为dont_starve_together_dedicated_server_scripts的文件夹, 并且进入这个文件夹

    mkdir dont_starve_together_dedicated_server_scripts && cd dont_starve_together_dedicated_server_scripts

创建一个update_dedicated_server.sh,  并且将Steamcmd下载命令写入

    touch update_dedicated_server.sh && echo 'steamcmd +login anonymous +app_update 343050 validate +quit' >> update_dedicated_server.sh

赋予update_dedicated_server.sh执行权限

    chmod u+x update_dedicated_server.sh

执行它开始下载服务端

    ./update_dedicated_server.sh

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/update-dedicated-server.png)

## 3.获取专用服务器Token
打开你的饥荒联机版，登陆游戏
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/get-token.png)
点击左下角的'账号'，会打开你的饥荒联机版账号信息
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/get-token-2.png)
点击游戏
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/get-token-3.png)
点击《饥荒：联机版》的游戏服务器
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/get-token-4.png)
添加新服务器，输入一个服务器名称，然后点击添加新服务器
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/get-token-5.png)
复制这串pds-g^开头的token，等会需要使用。

***为什么需要这一串token？因为服务器需要token标识这个服务器属于你***

## 4.创建(上传)存档文件
在根目录下创建一个名为.klei的隐藏文件(在Linux中，开头带.的文件(夹)会被自动隐藏。)

    mkdir ~/.klei

然后再在.klei下创建一个名为DoNotStarveTogether的文件夹，用于存放饥荒联机版的存档文件夹(Linux默认存放都是这个目录路径)

    mkdir ~/.klei/DoNotStarveTogether

打开你的饥荒联机版，登陆游戏 ***(不能离线登陆)***

创建一个存档
修改需要的设置(例如关掉挨千刀的草蜥蜴)
添加需要游玩的模组(不玩模组可以不加)
添加洞穴

确认无误之后，点击生成世界
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/mk-cluster.png)
生成完后退出世界

来到选择存档的界面，点击管理存档。
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/mk-cluster-2.png)
再点击打开世界文件夹。
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/mk-cluster-3.png)
在世界文件夹创建一个名为cluster_token.txt的文本文件, 填入刚刚你申请的token保存关闭(注意不要有空格)
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/mk-cluster-4.png)
回到Linux服务器，在DoNotStarveTogether下创建一个名为MyDediServer的文件夹

    mkdir ~/.klei/DoNotStarveTogether/MyDediServer

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/mk-cluster-5.png)
使用SFTP工具(我这里使用的是Tabby自带的SFTP上传工具)，将Master Caves cluster.ini cluster_token.txt上传到Linux服务器的MyDediServer，以下是文件夹结构

    MyDediServer
    ├── Caves 洞穴世界数据文件夹
    │   ├── backup 世界数据备份文件夹
    │   ├── leveldataoverride.lua 世界配置文件
    │   ├── modoverrides.lua 模组配置文件
    │   ├── save 世界数据文件夹
    │   ├── server_chat_log.txt 聊天记录文件
    │   ├── server.ini 次要服务器配置文件(如端口，是否是主世界等)
    │   └── server_log.txt 洞穴服务器日志文件
    ├── cluster.ini 主要服务器配置文件(如玩家数量，密码等)
    ├── cluster_token.txt 服务器token文件
    └── Master 地上世界数据文件夹
        ├── backup 世界数据备份文件夹
        ├── leveldataoverride.lua 世界配置文件
        ├── modoverrides.lua 模组配置文件
        ├── save 世界数据文件夹
        ├── server_chat_log.txt 聊天记录文件
        ├── server.ini 次要服务器配置文件(如端口，是否是主世界等)
        └── server_log.txt 地上服务器日志文件

## 5.下载模组&安装模组(没有模组可跳过)
找到你的Steamcmd目录，依次进入
steamapps-common-Don't Starve Together Dedicated Server-mods
使用编辑dedicated_server_mods_setup.lua文件

    vim dedicated_server_mods_setup.lua

调用官方的模组下载接口ServerModSetup，每个模组都有一个ID

    ServerModSetup("ID")

回到存档MyDediServer文件夹，进入Master文件夹，打开modoverrides.lua模组配置文件，其中有workshop-开头的代码，后面接的就是模组的ID
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/set-mods-2.png)
![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/set-mods.png)

写入保存后，开启服务器的时候会下载更新模组

***未知Bug***
现版本的饥荒联机版服务器无法下载模组
解决办法:
运行以下命令, 将饥荒联机版服务端的linux64中的steamclient.so替换掉饥荒联机版服务端64位运行库的steamclient.so

    cp ~/Steam/steamapps/common/Don't Starve Together Dedicated Server/linux64/steamclient.so ~/Steam/steamapps/common/Don't Starve Together Dedicated Server/bin64/lib64/

参考了贴吧用户**六神零号机**的解决帖子

## 6.创建启动脚本&运行脚本
启动之前先执行命令开启饥荒联机版服务器需要的默认10999和10998端口
***如果你使用的是云服务商提供的服务器，那么还需要在云服务商提供的控制台，修改防火墙规则，允许通过10999和10998端口***

    ufw allow 10999 && ufw allow 10998

配合screen命令进行使用方便管理

    apt-get install screen

在dont_starve_together_dedicated_server_scripts下创建两个分别名为start_master_server.sh和start_cave_server.sh的可执行文件

    touch start_master_server.sh && touch start_cave_server.sh

赋予执行权限

    chmod u+x start_master_server.sh && chmod u+x start_cave_server.sh

将执行命令写入到执行脚本中
地上世界start_master_server.sh

    cd ~/Steam/steamapps/common/Don\'t\ Starve\ Together\ Dedicated\ Server/bin64/
    screen -S Master ./dontstarve_dedicated_server_nullrenderer_x64 -console -cluster MyDediServer -shard Master

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/start-scripts.png)

洞穴世界start_cave_server.sh

    cd ~/Steam/steamapps/common/Don\'t\ Starve\ Together\ Dedicated\ Server/bin64/
    screen -S Master ./dontstarve_dedicated_server_nullrenderer_x64 -console -cluster MyDediServer -shard Caves

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/start-scripts-2.png)

启动地上世界

    ./start_master_server.sh

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/start-scripts-4.png)

依次按下Ctrl+A+D退出当前窗口
启动地下世界

    ./start_cave_server.sh

![](https://raw.githubusercontent.com/x-cast-x/x-cast-x.github.io/main/source/img/screenshots/start-a-donotstarvetogether-server/start-scripts-3.png)

日志提示'[Shard] secondary shard LUA is now ready! Sim paused'则是服务器启动成功，世界已暂停。
现在就可以打开饥荒饥荒联机版，在多人游戏中搜索你的世界名称加入游玩了。

# 参考链接
[Steamcmd官网](https://developer.valvesoftware.com/wiki/Zh/SteamCMD)
[有关最近饥荒专服不下载MOD的问题](https://tieba.baidu.com/p/9251408506)
[Klei官方教程](https://forums.kleientertainment.com/forums/topic/64441-dedicated-server-quick-setup-guide-linux/)
