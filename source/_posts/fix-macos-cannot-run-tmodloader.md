---
title: 修复MacOS无法运行tModLoader
banner_img: /img/bg_image/too_any_losing_heroines/run.jpg
tags: 
    - 泰拉瑞亚
    - tModLoader
    - 游戏
    - MacOS
categories: 
    - 折腾
---

# 解决方法:
打开terminal，输入运行:

    sudo chown -R $(whoami) ~/Library/Application\ Support/Steam/steamapps/common/tModLoader
    sudo chown -R $(whoami) ~/Library/Application\ Support/Terraria

# 适用场景:
• tModLoader无权限访问../tModLoader-Logs下的日志文件
• tModLoader无权限访问../Terraria下的存档文件

***如还无法运行tModLoader, 请查阅其它解决方法***