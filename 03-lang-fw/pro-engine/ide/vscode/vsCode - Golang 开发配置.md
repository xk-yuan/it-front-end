
```
[插件]

	：https://github.com/microsoft/vscode-go

	：https://marketplace.visualstudio.com/items?itemName=ms-vscode.Go

[使用]

	：https://code.visualstudio.com/docs/languages/go

```

### 01 ext install ms-vscode.Go

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1559126543068-921dc2ff-f82a-49ba-9c42-512b262e03bb.png#align=left&display=inline&height=325&name=image.png&originHeight=325&originWidth=654&size=77934&status=done&width=654)

### 02 go-delve/delve =>  GO 调试工具 => [vsCode - DLV [GO DEBUG TOOL]](https://www.yuque.com/back_end/course/tdzwo9)

### 03 安装常用插件

```
Colorization 代码着彩色
Completion Lists 代码自动完成（使用gocode）
Snippets  代码片段
Quick Info 快速提示信息（使用godef）
Goto Definition 跳转到定义（使用godef）
Find References  搜索参考引用（使用go-find-references）
File outline 文件大纲（使用go-outline）
Workspace symbol search 工作区符号搜索（使用 go-symbols）
Rename 重命名（使用gorename）
Build-on-save 保存构建（使用go build和go test）
Format 代码格式化（使用goreturns或goimports或gofmt）
Add Imports  添加引用（使用 gopkgs）
Debugging 调试代码（使用delve）
```

#### 安装方式一 [GO开发调试时, VSCode依赖工具]

```
[gocode - 代码自动补全]

	：go get -u -v github.com/nsf/gocode                                     # OK
  
  # https://github.com/mdempsky/gocode

[godef - 跳转到声明]

  ： go get -u -v github.com/rogpeppe/godef                            # OK

	# https://github.com/rogpeppe/godef

[golint - 就是lint]

  ：go get -u -v github.com/golang/lint/golint # F
  
  # https://golang.org/x/lint/golint

[go-find-references]

  ：go get -u -v github.com/lukehoban/go-find-references  # OK

[go-outline - 在当前文件中查找]

  ：go get -u -v github.com/lukehoban/go-outline # OK
  
  # https://github.com/ramya-rao-a/go-outline

[goreturns - 格式化代码]

  ：go get -u -v sourcegraph.com/sqs/goreturns
  
  # https://github.com/sqs/goreturns

[gopkgs - 自动补全未导入包]

  ：go get -u -v github.com/tpng/gopkgs  # OK
  
  # https://github.com/uudashr/gopkgs

[go-symbols - 在项目路径下查找]

  ：go get -u -v github.com/newhook/go-symbols # F
  
  # https://github.com/acroca/go-symbols

[gorename - 重命名符号]

  ：go get -u -v golang.org/x/tools/cmd/gorename   # F
  
  # https://golang.org/x/tools/cmd/gorename

[guru - 查询所有引用]

	：https://golang.org/x/tools/cmd/guru

[godoc - 鼠标悬浮时文档提示]

	：https://golang.org/x/tools/cmd/godoc

[dlv - 调试功能]

	：https://github.com/derekparker/delve/tree/master/cmd/dlv

[gomodifytags - 修改结构体标签]

	：https://github.com/fatih/gomodifytags

[goplay - 运行当前go文件]

	：https://github.com/haya14busa/goplay/
 
[impl - 新建接口]

	：https://github.com/josharian/impl

[gotype-live - 类型诊断]

	：https://github.com/tylerb/gotype-live

[gotests - 单元测试]

	：https://github.com/cweill/gotests/

[go-langserver - 语言服务]

	：https://github.com/sourcegraph/go-langserver

[filstruct - 结构体成员默认值]

	：https://github.com/davidrjenni/reftools/tree/master/cmd/fillstruct
```

#### 安装方式 二

```


[]

  -> %GOPATH%/src/golang/x # 解压到此文件夹下 # mv tools-master/  $GOPATH/src/golang/x/tools

 ：https://github.com/golang/lint

：git clone https://github.com/golang/lint.git # 手动下载lint包

-> 分别 拷贝 到 => %GOPATH%/src/github.com/ 和 %GOPATH%/src/golang/x 

src
├──  github.com
│        │ 
│        └─── lint            # copy   -> %GOPATH%/src/github.com/
└── golang
            └── x
                   ├── tools      # 解压到此目录下
                   └── lint         # copy    -> %GOPATH%/src/golang/x
                   
  ：手动安装 => go install github.com/lint
```

```
[创建目录]

	：$GOPATH/src/golang.org/x

[克隆golang.org工具源码 - src/golang.org/x/tools]

	：https://github.com/golang/tools

	：git clone https://github.com/golang/tools.git  # 手动下载tools包
  
  ：git clone https://github.com/golang/lint.git

```

```
[下载github源码]

	：以下手动下载

[下载 - $GOPATH/src/golang.org/x]

	：git clone http://github.com/golang/tools      # F

	：git clone http://github.com/golang/lint          # OK

	：git clone http://github.com/golang/net           # OK

	：git clone http://github.com/golang/text          # F

	：git clone http://github.com/golang/crypto     # F

	：git clone http://github.com/golang/sys           # F

[安装 - $GOPATH]

	：go get -u -v github.com/nsf/gocode

	：go get -u -v github.com/sqs/goreturns

	：go get -u -v github.com/golang/lint/golint

	：go get -u -v github.com/newhook/go-symbols

	：go install golang.org/x/tools/cmd/guru

	：go install golang.org/x/tools/cmd/gorename

	：go get -u -v github.com/rogpeppe/godef

	：go get -u -v github.com/lukehoban/go-outline

	：go get -u -v github.com/derekparker/delve/cmd/dlv

[集成到系统环境]

	：sudo cp -af $GOPATH/bin/* /usr/local/go/bin/ # 安装到临时目录, 然后拷贝编译后的命令到工作目录
```

```
go get -v github.com/ramya-rao-a/go-outline
go get -v github.com/acroca/go-symbols
go get -v github.com/mdempsky/gocode
go get -v github.com/rogpeppe/godef
go get -v github.com/zmb3/gogetdoc
go get -v github.com/fatih/gomodifytags
go get -v sourcegraph.com/sqs/goreturns
go get -v github.com/cweill/gotests/...
go get -v github.com/josharian/impl
go get -v github.com/haya14busa/goplay/cmd/goplay
go get -v github.com/uudashr/gopkgs/cmd/gopkgs
go get -v github.com/davidrjenni/reftools/cmd/fillstruct
go get -v github.com/alecthomas/gometalinter

go install github.com/ramya-rao-a/go-outline
go install github.com/acroca/go-symbols
go install github.com/mdempsky/gocode
go install github.com/rogpeppe/godef
go install github.com/zmb3/gogetdoc
go install github.com/fatih/gomodifytags
go install sourcegraph.com/sqs/goreturns
go install github.com/cweill/gotests/...
go install github.com/josharian/impl
go install github.com/haya14busa/goplay/cmd/goplay
go install github.com/uudashr/gopkgs/cmd/gopkgs
go install github.com/davidrjenni/reftools/cmd/fillstruct
go install github.com/alecthomas/gometalinter
$GOPATH/bin/gometalinter --install
go install golang.org/x/tools/cmd/godoc
go install golang.org/x/lint/golint
go install golang.org/x/tools/cmd/gorename
go install golang.org/x/tools/cmd/goimports
go install golang.org/x/tools/cmd/guru
```

**

