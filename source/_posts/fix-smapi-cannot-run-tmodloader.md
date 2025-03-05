---
title: 修复MacOS无法运行smapi
banner_img: /img/bg_image/too_any_losing_heroines/run.jpg
tags: 
    - 星露谷物语
    - 游戏
    - MacOS
categories: 
    - 折腾
---

# 解决方法:
启用macOS安全权限
进入系统设置>隐私和安全。
确保你的开发人员工具可见
![](https://stardewvalleywiki.com/mediawiki/images/9/9b/Fix_macOS_security_permissions_1.png)
如果你没有看到开发人员工具
打开你的terminal，输入运行以下命令:

    spctl developer-mode enable-terminal

单击开发人员工具
将终端添加到列表中，并启用它
![](https://stardewvalleywiki.com/mediawiki/images/b/b0/Fix_macOS_security_permissions_2.png)
如果你使用的是iTerm, 或其它终端, 那么也将它添加到开发人员工具列表中
如果使用类似于Stardrop和mod管理器, 也将它添加到开发人员工具列表中

最后重新安装smapi尝试运行它

***如仍然无法运行, 请查阅其它解决方法***

# 参考链接
[SMAPI官方文档](https://stardewvalleywiki.com/Modding:Installing_SMAPI_on_Mac)
