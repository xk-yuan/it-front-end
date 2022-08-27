### 基础项目工程搭建

```
[初始化 Node.js 项目]

	: npm init

[安装 hapi 模块]

	: npm i hapi@16 # V16 版本

[app.js]

// app.js
const Hapi = require('hapi');

const server = new Hapi.Server();
// 配置服务器启动 host 与端口
server.connection({
  port: 3000,
  host: '127.0.0.1',
});

const init = async () => {
  server.route([
    // 创建一个简单的 hello hapi 接口
    {
      method: 'GET',
      path: '/',
      handler: (request, reply) => {
        reply('hello hapi');
      },
    },
  ]);
  // 启动服务
  await server.start();
  console.log(`Server running at: ${server.info.uri}`);
};

init();

[启动]

	: node app.js # supervisor app.js

[访问]

	: http://127.0.0.1:3000
```

### 结构化项目工程重构

```
[项目工程化设计原则]

	: 单业务模块化 # 相同的业务需求, 归纳进单个模块
  
  : 模块二百行原则 # 通过模块 require 的方式形成关联，以保持各模块代码的相对精简与可维护性
  
  : 同类模块分组化 # 分组在本文中一般指形成一个文件目录，来对一些功能相似的业务模块形成管理
  
  : 配置文件分离

[重构工程目录]

├── config                       # 项目配置目录
|   ├── index.js                 # 配置项目中的配置信息
├── models                       # 数据库 model
├── node_modules                 # node.js 的依赖目录
├── plugins                      # 插件目录
├── routes                       # 路由目录
│   ├── hello-world.js           # 测试接口 hello-world
├── utils                        # 工具类相关目录
├── app.js                       # 项目入口文件
├── package.json                 # JS 项目工程依赖库
├── readme.md                    # 项目工程如何被使用的说明手册

```

```
[ 分离路由配置]

// routes/hello-hapi.js
module.exports = [
  {
    method: 'GET',
    path: '/',
    handler: (request, reply) => {
      reply('hapi');
    }
  }
]

[分离 config 基础参数配置]

// config/index.js
module.exports = {
  host: '127.0.0.1',
  port: 3000,
}

[关联 config 与 route 路由模块]

// APP 入口的 JS
const Hapi = require('hapi');
const config = require('./config');
const routesHelloHapi = require('./routes/hello-hapi');

const server = new Hapi.Server();
// 配置服务器启动 host 与端口
server.connection({
  port: config.port,
  host: config.host,
});

const init = async () => {
  server.route([
    // 创建一个简单的 hello hapi 接口
    ...routesHelloHapi,
  ]);
  // 启动服务
  await server.start();
  console.log(`Server running at: ${server.info.uri}`);
};

init();

```

```
[环境配置]

  // 引入一个被 .gitignore 的 .env 的文件，以 key-value 的方式，记录系统中所需要的可配置环境参数
  // .env.example 的示例配置文件用来放置占位

# .env.expamle
# 服务的启动名字和端口，但也可以缺省不填值，默认值的填写只是一定程度减少起始数据配置工作
HOST = 127.0.0.1
PORT = 3000

# .env
# 服务的启动名字和端口
HOST = 127.0.0.1
PORT = 3000

[读取 .env 中的配置值]

# 系统全局安装
supervisor
npm i env2

// app.js
require('env2')('./.env')

// config/index.js
const { env } = process;
module.exports = {
  host: env.HOST,
  port: env.PORT,  
}
```

### 接口文档 [hapi-swagger & Joi]

#### swagger 接口文档配置

```
[Swagger 插件配置]

# 安装适配 hapi v16 的 swagger 插件
npm i hapi-swagger@7
npm i inert@4
npm i vision@4
npm i package

├── plugins                       # hapi 插件配置
|   ├── hapi-swagger.js           # swagger 插件

// plugins/hapi-swagger.js
const inert = require('inert');
const vision = require('vision');
const package = require('package');
const hapiSwagger = require('hapi-swagger');

module.exports = [
  inert,
  vision,
  {
    register: hapiSwagger,
    options: {
      info: {
        title: '接口文档',
        version: package.version,
      },
      // 定义接口以 tags 属性定义为分组
      grouping: 'tags',
      tags: [
        { name: 'tests', description: '测试相关' },
      ]
    }
  }
]

// app.js 中，我们通过 server.register 挂载 swagger 插件配置

// app.js

const Hapi = require('hapi');
require('env2')('./.env');
const config = require('./config');
const routesHelloHapi = require('./routes/hello-hapi');
// 引入自定义的 hapi-swagger 插件配置
const pluginHapiSwagger = require('./plugins/hapi-swagger');

const server = new Hapi.Server();
// 配置服务器启动host与端口
server.connection({
  port: config.PORT,
  host: config.HOST,
});

const init = async () => {
  await server.register([
    // 为系统使用 hapi-swagger
    ...pluginHapiSwagger,
  ]);

  server.route([
    // 创建一个简单的hello hapi接口
    ...routesHelloHapi,
  ]);
  // 启动服务
  await server.start();
  console.log(`Server running at: ${server.info.uri}`);
};

init();
```

```
[]

	// REST接口添加Swagger标记, 在路由配置中的config字段增加tags:['api']即可将路由暴露为Swagger文档

// routes/hello-hapi.js
module.exports = [
  {
    method: 'GET',
    path: '/',
    handler: (request, reply) => {
      reply('hello hapi');
    },
    config: {
      tags: ['api', 'tests'],
      description: '测试hello-hapi',
    },
  },
];

[]

	: http://127.0.0.1:3000/documentation

[结合业务实现业务接口]

// routes/shops.js
const GROUP_NAME = 'shops';

module.exports = [
  {
    method: 'GET',
    path: `/${GROUP_NAME}`,
    handler: async (request, reply) => {
      reply();
    },
    config: {
      tags: ['api', GROUP_NAME],
      description: '获取店铺列表',
    },
  },
  {
    method: 'GET',
    path: `/${GROUP_NAME}/{shopId}/goods`,
    handler: async (request, reply) => {
      reply();
    },
    config: {
      tags: ['api', GROUP_NAME],
      description: '获取店铺的商品列表',
    },
  },
];

//
const GROUP_NAME = 'orders';

module.exports = [
  {
    method: 'POST',
    path: `/${GROUP_NAME}`,
    handler: async (request, reply) => {
      reply();
    },
    config: {
      tags: ['api', GROUP_NAME],
      description: '创建订单',
    },
  },
  {
    method: 'POST',
    path: `/${GROUP_NAME}/{orderId}/pay`,
    handler: async (request, reply) => {
      reply();
    },
    config: {
      tags: ['api', GROUP_NAME],
      description: '支付某条订单',
    },
  },
];
```

#### Joi 校验数据结构

```
[]

# 安装适配 hapi v16 的 joi 插件
npm i joi@13

[适用于动态路由的 params 验证]

  // 动态路由所依赖的变量 orderId 以 params 属性的字段来传递
  // orderId: Joi.string().required() 的描述，定义了 orderId 必须是字符串，且此参数必填
{
	method: 'POST',
	path: `/${GROUP_NAME}/{orderId}/pay`,
	config: {
		validate: {
			params: {
				orderId: Joi.string().required(),
			}
		}
	}
},

{
    "error": "Bad Request",
    "message": "此处会有明确的字段验证错误描述",
    "statusCode": 400
}

[适用于 POST 接口的 payload（request body）验证]

	// 此类的参数校验可以通过 validate.payload 来约束

// 入参的数据
[
  { goods_id: 123, count: 1 },  // 1件 id 为 123 的商品
  { goods_id: 124, count: 2 },  // 2件 id 为 124 的商品
]

// 对应的嵌套入参校验
validate: {
  payload: {
    goodsList: Joi.array().items(
      Joi.object().keys({
        goods_id: Joi.number().integer(),
        count: Joi.number().integer(),
      })
    )
  }
}

[适用于 GET 接口的 query（URL 路径参数）]

  // 此类的参数校验可以通过 validate.query 来约束

validate: {
  query: {
    limit: Joi.number().integer().min(1).default(10)
      .description('每页的条目数'),
    page: Joi.number().integer().min(1).default(1)
      .description('页码数'),
  }
}

[适用于 header 额外字段约束的 headers 验证]

  // 基于 JWT 的用户身份验证，会依赖 header 中的 authorization 字段的配置
  // 但由于 header 中本身还涵盖了其他的字段属性，所以需要用 unknown 来做一个冗余处理

validate: {
  headers: Joi.object({
    authorization: Joi.string().required(),
  }).unknown(),
}

```

