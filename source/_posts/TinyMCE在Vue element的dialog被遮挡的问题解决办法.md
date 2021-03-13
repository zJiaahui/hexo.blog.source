---
title: TinyMCE在Vue element的dialog被遮挡的问题解决办法.md
tags: 
    - vue
    - tinymce 5.X
    - element ui
---
找到使用了 el-dialog的组件重写dialog 的tox-tinymce-aux样式
```css
.tox-tinymce-aux {
    z-index: 5000 !important;
  }
```