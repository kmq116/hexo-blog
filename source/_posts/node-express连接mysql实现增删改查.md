---
title: node-express连接mysql实现增删改查
date: 2021-02-16 10:37:26
tags: 
- Nodejs学习
- 后端入门
- 
categories: Nodejs
---
继上一篇的代码
在`index.js`的同级目录下新建一个`router.js`和`mysql.js`文件
### 连接数据库
终端执行 `npm install --save mysql`安装`mysql`模块
在`mysql.js`中封装一个简单的数据库查询的方法
代码如下：
```JavaScript
// 连接数据库
const mysql = require("mysql");
const config = {
  host: "localhost",
  user: "root",
  password: "linux0.1",
  database: "mydb",
};
const client = mysql.createConnection(config);
// sql语句
function sqlQuery(sql, callback) {
  client.query(sql, (err, result) => {
    if (err) {
      return console.log("错误");
    }
    callback(result);
  });
}
module.exports = sqlQuery;
```
config是一个对象，里面的信息是数据库的用户名，密码，要用的数据库名，配置好后，调用`mysql.createConnection()`方法与数据库进行连接
下面的函数调用的是mysql模块提供的`query`方法，他接收两个参数，一个是sql语句，另一个为一个回调函数，
将这个函数写好后，从页面中将该方法导出
### 路由配置
在`router.js`中写入如下代码
```JavaScript
const express = require("express");
const router = express.Router();
const sqlQuery = require("./mysql");
//设置跨域访问
router.all("*", function (req, res, next) {
  //设置允许跨域的域名，*代表允许任意域名跨域
  res.header("Access-Control-Allow-Origin", "*");
  //允许的header类型
  res.header("Access-Control-Allow-Headers", "content-type");
  //跨域允许的请求方式
  res.header("Access-Control-Allow-Methods", "DELETE,PUT,POST,GET,OPTIONS");
  if (req.method.toLowerCase() == "options") res.sendStatus(200);
  //让options尝试请求快速结束
  else next();
});
// 查询userinfo表
router.get("/", (req, res) => {
  const sql = "select * from userinfo";
  sqlQuery(sql, (data) => {
    res.send({
      code: "200",
      message: "查询成功",
      data,
    });
  });
});
// 登录
router.post("/api/auth/login", function (req, res) {
  const { username, password } = { ...req.body };
  const sql = `select * from userinfo where username='${username}' and password='${password}'`;
  sqlQuery(sql, (data) => {
    if (data.length > 0)
      return res.send({
        code: "200",
        result: { token: "4291d7da9005377ec9aec4a71ea837f" },
        message: "登录成功",
      });
    res.send({
      code: "500",
      message: "用户不存在",
    });
  });
});
// 注册
router.post("/api/register", (req, res) => {
  const { username, password } = { ...req.body };
  const sql = `select * from userinfo where username='${username}'`;
  sqlQuery(sql, (data) => {
    if (data.length == 0) {
      const sql = `insert into userinfo values('${username}',null,'${password}')`;
      sqlQuery(sql, (data) => {
        res.send({
          code: "200",
          message: "注册成功",
        });
      });
    } else {
      res.send({
        code: "500",
        message: "用户已经存在",
      });
    }
  });
});
// 修改密码
router.post("/api/passwordChange", (req, res) => {
  const { username, password, newPassword } = { ...req.body };
  const sql = `select * from userinfo where username='${username}' AND password='${password}' `;
  sqlQuery(sql, (data) => {
    if (data.length != 0) {
      const sql = `update userinfo set password='${newPassword}' where username = '${username}'`;
      sqlQuery(sql, (data) => {
        res.send({
          code: "200",
          message: "修改成功",
        });
      });
    } else {
      res.send({
        code: "500",
        message: "用户名或原密码不正确",
      });
    }
  });
});
module.exports = router;
```
### 运行服务
先引入封装好的执行sql语句的方法
修改主入口文件`index.js`
```javascript
const express = require("express");
const app = express();
const port = 3000;
const router = require("./router");
app.use(express.json())
app.use("/", router);
app.listen(port, () => console.log(`Example app listening on port port!`));
```
终端执行`node index.js`
服务就跑起来了，这时使用postman 或者前端页面来调用我们写好的接口，传入对应的参数就ok了！！！