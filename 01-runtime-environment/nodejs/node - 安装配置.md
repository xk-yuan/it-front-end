
```java
[下载]

	：wget https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz
    
	：tar xf node-v10.15.3-linux-x64.tar.xz
    
    ：cd node-v10.15.3-linux-x64
    
    ：/bin/node -v  # 查看版本

[配置环境]

	：ln -s .../nodejs/bin/npm   /usr/local/bin/ 
        
    ：ln -s .../nodejs/bin/node   /usr/local/bin/

```

```java
[源码安装]

	：git clone https://github.com/nodejs/node.git
    
	：chmod -R 755 node
    
    ：cd node
    
    ：./configure && make && make install
    
    ：node --version

[ubuntu 平台安装]

	：apt-get install nodejs
    
    ：apt-get install npm

```

环境配置

```
[node_global]

	：npm config set prefix "D:\cache\nodeRepository\node_global" # 全局安装路径

[node_cache]

  ：npm config set cache "D:\cache\nodeRepository\node_cache"   # 全局缓存路径

  : yarn config set global-folder "D:\cache\nodeRepository\yarn_global" # 全局安装路径
  : yarn config set cache-folder "D:\cache\nodeRepository\yarn_cache"   # 全局缓存路径

[环境]

	：NODE_HOME=
  
  ：PATH=..;%NODE_HOME%\

	：NODE_PATH=D:\cache\nodeRepository\node_global\node_modules
  
  ：PATH=...;%NODE_PATH%/
```

国内源

```
[安装淘宝镜像]

	：npm install -g cnpm --registry=https://registry.npm.taobao.org

[run]

	：cnpm -v
```

