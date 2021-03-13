---
title: VUE 实现复制内容到剪贴板功能
tags:
    - VUE
---
安装插件

```
npm install vue-clipboard2 --save
```
main.js中全局注入

```
import VueClipboard from 'vue-clipboard2'

Vue.use(VueClipboard)
```

使用

```

三、使用

```
<ul class="file-list">
  <li v-for="(f, index) of files" :key="index">
    <span>[文件{{index + 1}}] {{f}}</span>
    <span v-clipboard:copy="要复制的内容" v-clipboard:success="onCopy" v-clipboard:error="onError">复制</span>
  </li>
</ul>
```