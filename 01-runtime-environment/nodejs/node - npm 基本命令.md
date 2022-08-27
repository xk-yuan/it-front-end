### 常见命令参数

```
[模块安装命令解析]

	: npm install module

[npm install module]

	# 会把module包安装到node_modules目录中
  # 不会修改package.json 
  # 运行npm install 命令时, 不会自动安装module包
	> npm install module

[npm install module --save]

  # 会把module包安装到node_modules目录汇总
  # 会修改package.json, 将模块名和版本号添加到dependencies部分
  // dependencies 上线环境的依赖包
  # 运行npm install 命令时，会自动安装module包, 线上环境运行时会将包安装
	> npm install module --save


[npm install module --save-dev]

	# 会把module包安装到node_modules目录汇总
  # 会修改package.json，将模块名和版本号添加到devDependencies部分
	// devDependencies 测试环境的依赖包
  # 运行npm install 命令时, 会自动安装module包
  # 线上环境并不会进行安装
  > npm install module --save-dev

```

