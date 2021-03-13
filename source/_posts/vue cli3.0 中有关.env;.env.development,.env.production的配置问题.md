---
title: vue cli3.0 中有关.env;.env.development,.env.production的配置问题.md
tags:
    - vue
---
1，关于文件名：必须以如下方式命名，不要乱起名，也无需专门手动控制加载哪个文件

　　`.env` 全局默认配置文件，不论什么环境都会加载合并

　　`.env.development` 开发环境下的配置文件

　　`.env.production` 生产环境下的配置文件

2，关于内容

　　注意：属性名必须以`VUE_APP_`开头，比如`VUE_APP_XXX` 不然无法加载

3，关于文件的加载：

　　根据启动命令vue会自动加载对应的环境，vue是根据文件名进行加载的，所以上面说“不要乱起名，也无需专门控制加载哪个文件”比如执行npm run serve命令，会自动加载.env.development文件

注意：.env文件无论是开发还是生成都会加载的公用文件　
如过我们运行npm run serve 在就先加载.env文件，之后加载.env.development文件，两个文件有同一个项，则，后加载的文件就会覆盖掉第一个文件，也即是.env.development文件覆盖掉了.env文件的NOOE_ENV选项。同理如果npm run build 就执行了.env和.env.development。