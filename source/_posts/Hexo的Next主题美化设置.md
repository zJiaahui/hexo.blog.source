---
title: Hexo的Next主题美化设置
date: 2020-09-29 11:06:15
tags: Hexo
---

Hexo的Next主题美化主要是通过该主题目录下的 `_config.yml` 配置文件来完成的，下面我们呢就来通过修改 `_config.yml ` 配置文件来对Next主题进行简单的美化...
<!-- more -->
- #### 1.选择next主题的布局方式（该主题有四种布局方式）
  >① 打开在博客项目的`themes`文件夹下找到next主题文件打开<br>②找到`_config.yml`文件打开<br>③在配置文件中搜索`Scheme`<br>④将想要主题前的`#`号去掉，把要替换的加上`#`号

  
    ```
    # Schemes
    #scheme: Muse
    scheme: Mist  
    #scheme: Pisces
    #scheme: Gemini
    ```

- #### 2.首页文章设置不显示全文
  >①这个直接在文章的md文件中指定位置加入代码`<!-- more -->`即表示后面的内容省略显示阅读全文按钮

- #### 3.首页菜单设置
  >①next默认只有两个页面菜单，首页home和归档archives, 
  >`_config.yml`文件中搜索`menu`我们按需选择

  
    ```
    menu:
    home: / || home #首页
    #about: /about/ || user #关于
    #tags: /tags/ || tags #标签
    #categories: /categories/ || th #分类
    archives: /archives/ || archive #归档
    #schedule: /schedule/ || calendar #日程表
    #sitemap: /sitemap.xml || sitemap #站点地图
    #commonweal: /404/ || heartbeat #公益404
    ```

  >除了首页和归档这两个菜单选项其他的都要手动创建对应的页面,输入如下命令会在`/source`下对应生成页面文件夹和里面的`index.md`
  
    ```
    hexo new page about
    ```

- #### 4.设置头像
    >在`source`目录下新建一个`images`目录，放一张名为`avatar.png`的头像，修改主题配置文件`_config.yml`的`avatar`字段后的`url`
    
      ```
      avatar:
          url: /images/avatar.png
      ```
- #### 5.设置博客favicon图标
    >在`/themes/next/source/images`目录下放置`.ico`图标，我这里放了两种大小的ico图标，然后在主题配置文件找到 `favicon` 并修改
    
      ```
      favicon: 
      small: /images/favicon-16x16.ico
      medium: /images/favicon-32x32.ico
      #apple_touch_icon: /images/apple-touch-icon-next.png
      #safari_pinned_tab: /images/logo.svg
      #android_manifest: /images/manifest.json
      #ms_browserconfig: /images/browserconfig.xml
      ```
- #### 6.侧边栏社交链接
    >在主题配置文件找到 `social` 把需要的取消注释，然后填好你的链接就可以了，||后面的是图标名称，和菜单的一样，也是使用Font Awesome图标名字。
    
      ```
      social:
          GitHub: https://github.com/yourname || github
          GMail: mailto:yourname@gmail.com || envelope
          #Google: https://plus.google.com/yourname || google
          #Twitter: https://twitter.com/yourname || twitter
          Facebook: https://www.facebook.com/ || facebook
          #VK Group: https://vk.com/yourname || vk
          #StackOverflow: https://stackoverflow.com/yourname || stack-overflow
          #YouTube: https://youtube.com/yourname || youtube
          #Instagram: https://instagram.com/yourname || instagram
      ```

- #### 7.设置背景动画
    >同样是主题配置文件，我这里用的是`canvas_nest`
    
    ```
    # Canvas-nest
    canvas_nest: true

    # three_waves
    three_waves: false

    # canvas_lines
    canvas_lines: false

    # canvas_sphere
    canvas_sphere: false
    ```
- #### 8.添加字数统计及阅读时长
  >①在博客根目录下用命令行输入如下代码安装 `hexo-symbols-count-time`

    ```
    npm install hexo-symbols-count-time --save
    
    ```
  >②修改博客根目录下的配置文件 `symbols_count_time`配置
    ```
    symbols_count_time:
    #文章内是否显示
    symbols: true
    time: true
    # 网页底部是否显示
    total_symbols: true
    total_time: true
    ```
  >③修改Next主题配置文件 `symbols_count_time`配置

  
    ```
    symbols_count_time:
    separated_meta: true  # 是否换行显示
    item_text_post: true  # 使用图标还是文本表示
    item_text_total: true # 博客底部统计字数统计阅读时长
    awl: 4
    wpm: 275
    ```
- #### 9.文章代码块增加快捷复制及主题设置
  >主题配置文件搜索 `copy_button` 进行如下配置
  
    ```
    copy_button:
    enable: true 
    # Show text copy result.
    show_result: true 
    # Available values: default | flat | mac
    style: mac #代码块风格设置mac风格
    ```
  >题配置文件搜索 `highlight_theme` 代码配置块主题
  
    ```
    codeblock:
    # Code Highlight theme
    # Available values: normal | night | night eighties | night blue | night bright | solarized | solarized dark | galactic
    # See: https://github.com/chriskempson/tomorrow-theme
    highlight_theme: night #默认normal
    ```

- #### 10.增加版权信息
  >主题配置文件搜索`creative_commons`，进行如下配置
  
    ```
    creative_commons:
    license: by-nc-sa
    sidebar: false #首页边栏是否显示
    post: true #文章底部是否显示
    ```
- #### 11.添加访问人数和总访问量
  >主题配置文件搜索 `busuanzi_count`，进行如下配置
  
    ```
    busuanzi_count:
    enable: true
    total_visitors: true
    total_visitors_icon: user
    total_views: true
    total_views_icon: eye
    post_views: true
    post_views_icon: eye
    ```

- #### 12.增加打赏功能
  >先把需要的收款码放到 `/themes/next/source/images`里面。

  >主题配置文件搜索搜索`reward_settings`进行如下配置 

  
    ```
    reward_settings:
    # If true, reward will be displayed in every article by default.
    enable: true
    animation: true
    #comment: Donate comment here.

    reward:
    wechatpay: /images/wechatpay.png
    alipay: /images/alipay.png
    #bitcoin: /images/bitcoin.png
    
    ```
