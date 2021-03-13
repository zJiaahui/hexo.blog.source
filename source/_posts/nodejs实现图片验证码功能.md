---
title: nodejs 实现图片验证码（svg-captcha）
tags:
    - nodejs 
    - web
---
在nodejs后端先准备一个获取图片动态验证码的路由，当访问该路由时则通过`svg-captcha`库生成svg验证码信息对象（该对象包含text：验证码文本，data:验证码svg信息）然后将text存储到express-session库中的session中，将data返回到客户端通过img标签形成图片验证码，即当客户端访问服务端时带上输入的验证码和服务端存储在session中的text进行对比即可


安装插件

```
npm install express-session
```
```
npm install --save svg-captcha
```


导入控件
```nodejs
const session = require('express-session');

const app = express()//创建服务对象
//必须在所有路由中间件之前使用该中间件
app.use(session({
    secret: constant.secretKey,  // 每一次在生成Cookie的时候，通过一个私钥生成一个字符串然后再交给客户端(读取我的配置文件里面的私钥key)
    resave: false,
    saveUninitialized: true,
    // cookie : {secure : true }
}));
```

```nodejs
const exprees = require('express')
const router = exprees.Router()
var svgCaptcha = require('svg-captcha')
router.get('/', (req, res) => {
    // 获取验证码
   const captcha = svgCaptcha.create({
        size: 6, //验证码长度
        fontSize: 45, //验证码字号
        noise: 2, //干扰线条数目
        width: 130, //宽度
        height: 36, //高度
        color: true, //验证码字符是否有颜色，默认是没有，但是如果设置了背景颜色，那么默认就是有字符颜色
        background: '#ccc' //beijing
    })
    // 把数据写入到session对象里面（第一次访问的话默认是没有验证码信息的）
    req.session.captcha = captcha.text;
    //console.log('获取验证码！', req.session.captcha)
    // 设置类型
    res.type('svg');
    // console.log(captcha.data)
    res.status(200).send(captcha.data);
})
module.exports = router
```

前端代码
```html
 <div class="captcha"><input type="text" placeholder="验证码" id="captcha" name="vcode">
                    <img src="/captcha" alt="" class="captcha-img" onclick='this.src="/captcha?"+new Date'
                        id="captcha-img">
                </div>
```

验证图片验证码
```
exports.doLogin = function (req, res, next) {
    // 1. 获取用户输入的参数信息
    let uname = req.body.uname;
    let pwd = req.body.pwd;
    let vcode = req.body.vcode;
    let session_vcode = req.session.captcha;

    if (!uname || !pwd || !vcode || !session_vcode) {
        return res.json({
            code : -1,
            msg : '请求解析失败'
        });
    }

    if (session_vcode && vcode.toLowerCase() !== session_vcode.toLowerCase()) {
        return res.json({
            code: 1001,
            msg: '验证码输入错误'
        });
    }  
}
```

