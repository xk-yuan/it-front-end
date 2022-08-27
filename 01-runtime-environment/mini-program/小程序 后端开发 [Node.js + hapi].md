    借助小程序 JavaScript 的动态语言灵活性与跨平台性，可以数日之内，便完成一款跨平台的接近原生体验的轻应用。而小程序只是高效地解决了产品前端的问题。

    目前主流的三种 Web 服务交互方案中，REST 相比于 SOAP（Simple Object Access Protocol，简单对象访问协议）以及 XML-RPC 更加简单明了，无论是对 URL 的处理还是对 Payload 的编码，REST 都倾向于用更加简单轻量的方法设计和实现。

```
[功能]

	: 用户权鉴与 业务的增删改查 [CURD]

[技术选型]

	: HApi

[调试]

	: console.log
  
  : Supervisor / nodemon / PM2 # 监视代码的改动然后自动重启
  # npm i -g supervisor
  # node app.js -> supervisor app.js
  
  : node-inspector + Chrome

```

| 方法 | 路径 | 是否需要登录 | 功能描述 |
| --- | --- | --- | --- |
| POST | /users/wx-login | 否 | 用户小程序授权登录 |
| GET | /shops | 否 | 店铺列表访问 |
| GET | /shops/{shopId}/goods | 否 | 某店铺商品列表访问 |
| POST | /orders | 是 | 创建购物订单，并获取订单编号 |
| POST | /orders/{orderId}/pay | 是 | 支付订单 |


### 前后端分离

![](../../imgs/1565054688410-9f8fe785-22e1-4152-8fc5-1b6edd0dbdc9.webp#align=left&display=inline&height=370&originHeight=634&originWidth=1280&size=0&status=done&width=746)

![](../../imgs/1565054726795-2a04449d-7a27-4fe9-8267-1ea80e214715.jpeg#align=left&display=inline&height=382&originHeight=708&originWidth=1384&size=0&status=done&width=746)

![](../../imgs/1565054750727-90b88a2d-0d50-4615-b1bb-8bf779519a96.webp#align=left&display=inline&height=556&originHeight=954&originWidth=1280&size=0&status=done&width=746)

| 类目 | Node.js | PHP | Go | Java |
| --- | --- | --- | --- | --- |
| 调试工具与技巧 | inspector+Chrome / VS Code | echo, dd, Xdebug | Log, Delve | intellij IDEA |
| 后端基础应用框架 | hapi | Laravel | gin | Spring Cloud\\Spring Boot |
| 一致化的 HTTP Response 返回 | boom | symfony/http-foundation | gin/Response Writer | ResponseBody + fastjson |
| 入参校验 | Joi | symfony/validator | gin/validator | JSR 303\\ Hibernate Validator |
| API Swagger文档化 | hapi-swagger | zircote/swagger-php | go-swagger | springfox-swagger-ui |
| 数据库 ORM | sequelize | Eloquent | gorm | JPA\\Hibernate |
| 基于 JWT 的用户身份验证 | hapi-auth-jwt2 | Laravel/passport | go-oauth2/oauth2 | spring-security-oauth2 |
| 数据缓存 | catbox | Illuminate\\Cache | go-cache | spring-boot-starter-cache |
| 日志系统 | good | monolog | sirupsen/logrus | slf4j\\ logback |
| 单元测试 | Lab & code | oh-unit | Go test | junit |




