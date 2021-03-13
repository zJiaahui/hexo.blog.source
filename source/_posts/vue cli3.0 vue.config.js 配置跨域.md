---
title: vue cli3.0 vue.config.js 配置跨域
tags:
    - vue
---
- 在当前项目的根路径下新建一个文件,文件名是固定的 vue.config.js
```vue
module.exports = {
    devServer: {
        open: true,
        host: 'localhost',
        port: 8090,
        https: false,
        //以上的ip和端口是我们本机的
        proxy: {//配置跨域
            '/api': {
                target: 'http://localhost:5000/api/',//要跨域请求的后台请求地址
                ws: true,
                changOrigin: true,//允许跨域
                pathRewrite: {
                    '^/api': ''//请求的时候使用这个api就可以
                }
            }
            
        }
    }
}

```
跨域页面使用:
后台的接口为5000；我们本地的接口为8090,所以我们需要去到vue.config.js配置跨域 http://localhost:5000/api/
```vue
    this.$axios.post('/api/users/login',this.user)
        .then(res =>{
            alert('登录成功')
        })
 
        }
```