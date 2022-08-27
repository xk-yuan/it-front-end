nvm —— 管理 Node 版本（包括下载 Node,切换 Node 版本）

```
[]

	: npm install -g nrm
  
  : nrm add name http://XXXXXX:4873 # 添加本地的npm镜像地址
  
  : nrm use name # 使用本址的镜像地址, name为你要增加的地址

[]
npm install -g sinopia 或者 yarn global add sinopia 
  
[]

	npm config set registry http://xxx.xx.xx.xx:4873/       
	//xxx.xx.xx.xx 为自己的ip 
  
[新建用户]

npm adduser
Username: test
Password: test
Email: (this IS public) xxx@xxxx

	: npm publish     // 在自己要发布的包 路径打这个命令

//
storage: 仓库保存的路径
htpasswd: 保存密码信息 只有新建用户后才 有这个文件
config.yaml: 这个是本地的 配置文件 信息（改这个）
```
```
// 本人配置文件

#
# This is the default config file. It allows all users to do anything,
# so don't use it on production systems.
#
# Look here for more config file examples:
# https://github.com/rlidwka/sinopia/tree/master/conf
#

# path to a directory with all packages
storage: ./storage    # npm包存放的路径

auth:
  htpasswd:
    file: ./htpasswd
    # Maximum amount of users allowed to register, defaults to "+inf".
    # You can set this to -1 to disable registration.
    # max_users: 1000
    max_users: 1000     # 默认为1000，改为-1，禁止注册

# a list of other known repositories we can talk to
uplinks:
  npmjs:
    url: http://registry.npm.taobao.org/  # 默认为npm的官网，由于国情，修改 url 让sinopia使用 淘宝的npm镜像地址

packages:
  '@*/*':
    # scoped packages
    access: $all
    publish: $authenticated

  '*':
    # allow all users (including non-authenticated users) to read and
    # publish all packages
    #
    # you can specify usernames/groupnames (depending on your auth plugin)
    # and three keywords: "$all", "$anonymous", "$authenticated"
    access: $all

    # allow all known users to publish packages
    # (anyone can register by default, remember?)
    publish: $authenticated

    # if package is not available locally, proxy requests to 'npmjs' registry
    # proxy: npmjs   #这个去掉的话,sinopia 将不去下载依赖包   如果只是要放自己资源仓库的话就去掉      
    # 

# log settings
logs:
  - {type: stdout, format: pretty, level: http}
  #- {type: file, path: sinopia.log, level: info}

# you can specify listen address (or simply a port) 
listen: 0.0.0.0:4873  # 默认没有，只能在本机访问，添加后可以通过外网访问。

```
