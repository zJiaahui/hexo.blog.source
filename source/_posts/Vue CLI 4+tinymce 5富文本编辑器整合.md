---
title: Vue CLI 4 + tinymce 5 富文本编辑器整合
tags: 
    - vue
    - tinymce 5.X
    - Vue CLI 4.X
---

基于Vue CLI 4脚手架搭建的项目整合tinymce 5富文本编辑器
<!--more-->
## 插件安装

- 如果有注册或购买过服务的话，直接通过组件配置api-key直接使用，没有注册或者购买的直接下载tinymce使用


#### 安装tinymce-vue

```
npm install @tinymce/tinymce-vue@3.2.0 -S

```
> 注意如果是使用的vue2.x请下载tinymce-vue@4.0.0以下的版本（tinymce-vue@4.0.0专门为vue3提供的）版本不对无法正常使用

#### 安装tinymce

```
npm install tinymce -S

```

#### 下载中文语言包

- 官网下载中文语言包（默认是英文）：https://www.tiny.cloud/get-tiny/language-packages/

#### 开始使用
- 1、在public目录下新建tinymce，将上面下载的语言包解压后将langs文件夹复制到该目录
- 2、在node_modules里面找到tinymce,将skins目录复制到public/tinymce里面

```vue
<template>
  <div class="tinymce-editor">
    <editor
      v-model="myValue"
      :init="init"
      :disabled="disabled"
      @onClick="onClick"
    >
    </editor>
    <div class="editor-content" v-html="myValue" />
  </div>
</template>
<script>
import tinymce from "tinymce/tinymce";
import Editor from "@tinymce/tinymce-vue";
import "tinymce/themes/silver";
import "tinymce/icons/default"; //图标
// 编辑器插件plugins
// 更多插件参考：https://www.tiny.cloud/docs/plugins/
import "tinymce/plugins/image"; // 插入上传图片插件
//import "tinymce/plugins/media"; // 插入视频插件
import "tinymce/plugins/table"; // 插入表格插件
import "tinymce/plugins/lists"; // 列表插件
import "tinymce/plugins/wordcount"; // 字数统计插件

import "tinymce/plugins/code"; //源代码
import "tinymce/plugins/preview"; //预览
import "tinymce/plugins/indent2em"; //首行缩进
import "tinymce/plugins/link"; //连接

export default {
  components: {
    Editor,
  },
  props: {
    value: {
      type: String,
      default: "",
    },
    // 基本路径，默认为空根目录，如果你的项目发布后的地址为目录形式，
    // 即abc.com/tinymce，baseUrl需要配置成tinymce，不然发布后资源会找不到
    baseUrl: {
      type: String,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    height: {
      type: [Number, String],
      required: false,
      default: 360,
    },
    plugins: {
      type: [String, Array],
      default: "lists image table wordcount code preview indent2em link ",
    },
    toolbar: {
      type: [String, Array],
      default() {
        return [
          "undo redo | bold italic forecolor backcolor | indent2em lineheight | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent ",
          "formatselect | fontselect | fontsizeselect | lists link image table | removeformat | preview | code",
        ];
      },
    },
  },
  computed: {
    containerWidth() {
      const width = this.width;
      if (/^[\d]+(\.[\d]+)?$/.test(width)) {
        // matches `100`, `'100'`
        return `${width}px`;
      }
      return width;
    },
  },
  data() {
    return {
      init: {
        language_url: `${this.baseUrl}/tinymce/langs/zh_CN.js`,
        language: "zh_CN",
        skin_url: `${this.baseUrl}/tinymce/skins/ui/oxide`,
        content_css: `${this.baseUrl}/tinymce/skins/content/default/content.css`,
        forced_root_block: "",
        // lineheight_formats:
        //   "8pt 9pt 10pt 11pt 12pt 14pt 16pt 18pt 20pt 22pt 24pt 26pt 36pt",
        fontsize_formats: "12px 14px 16px 18px 24px 36px 48px 56px 72px",
        font_formats:
          "微软雅黑='微软雅黑';宋体='宋体';黑体='黑体';仿宋='仿宋';楷体='楷体';隶书='隶书';幼圆='幼圆';Andale Mono=andale mono,times;Arial=arial,helvetica,sans-serif;Arial Black=arial black,avant garde;Book Antiqua=book antiqua,palatino;Comic Sans MS=comic sans ms,sans-serif;Courier New=courier new,courier;Georgia=georgia,palatino;Helvetica=helvetica;Impact=impact,chicago;Symbol=symbol;Tahoma=tahoma,arial,helvetica,sans-serif;Terminal=terminal,monaco;Times New Roman=times new roman,times;Trebuchet MS=trebuchet ms,geneva;Verdana=verdana,geneva;Webdings=webdings;Wingdings=wingdings",
        // skin_url: `${this.baseUrl}/tinymce/skins/ui/oxide-dark`, // 暗色系
        // content_css: `${this.baseUrl}/tinymce/skins/content/dark/content.css`, // 暗色系
        height: 300,
        plugins: this.plugins,
        toolbar: this.toolbar,
        link_title: false,
        image_description: false,
        branding: false,
        menubar: false,
        // 此处为图片上传处理函数，这个直接用了base64的图片形式上传图片，
        // 如需ajax上传可参考https://www.tiny.cloud/docs/configure/file-image-upload/#images_upload_handler
        // images_upload_handler: (blobInfo, success, failure) => {
        //   const img = "data:image/jpeg;base64," + blobInfo.base64();
        //   success(img);
        // },
      },
      myValue: this.value,
    };
  },
  mounted() {
    tinymce.init({});
  },
  methods: {
    // 添加相关的事件，可用的事件参照文档=> https://github.com/tinymce/tinymce-vue => All available events
    // 需要什么事件可以自己增加
    onClick(e) {
      this.$emit("onClick", e, tinymce);
    },
    // 可以添加一些自己的自定义事件，如清空内容
    clear() {
      this.myValue = "";
    },
  },
  watch: {
    value(newValue) {
      this.myValue = newValue;
    },
    myValue(newValue) {
      this.$emit("input", newValue);
    },
  },
};
</script>
<style scoped>
</style>
```