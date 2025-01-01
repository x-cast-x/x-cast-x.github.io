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

    ```bash
    sudo apt-get install lib32gcc1
    ```

用于下载你需要的模组

    ```bash
    sudo apt install steamcmd
    ```

***其它系统安装请阅读Steamcmd的官网***

输入steamcmd，尝试运行steamcmd，成功后输入exit退出
![](https://raw.githubusercontent.com/HarmonyTou/harmonytou.github.io/main/source/img/screenshots/start-a-tModloader-server/steamcmd.png)

## 2.获取饥荒联机版服务端

创建一个名为dont_starve_together_dedicated_server_scripts的文件夹, 并且进入这个文件夹

    ```bash
    mkdir dont_starve_together_dedicated_server_scripts && cd dont_starve_together_dedicated_server_scripts
    ```

创建一个update_dedicated_server.sh,  并且将Steamcmd下载命令写入

    ```bash
    touch update_dedicated_server.sh && echo 'steamcmd +login anonymous +app_update 343050 validate +quit' >> update_dedicated_server.sh
    ```

赋予update_dedicated_server.sh执行权限

    ```bash
    chmod u+x update_dedicated_server.sh
    ```

执行它开始下载服务端

    ```bash
    ./update_dedicated_server.sh
    ```
