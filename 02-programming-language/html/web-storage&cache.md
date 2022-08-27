
```
[本地存储, Local Storage]

  # 用户浏览器中对数据进行本地的存储
  // window.localStorage   存储没有截止日期的数据
  // window.sessionStorage 针对一个 session 来存储数据(浏览器标签关闭时清理)


[应用程序缓存 Application Cache]

	: HTML Cache Manifest
  // <html manifest="demo.appcache"> , 指定了 manifest 的页面在用户对其访问时都会被缓存
  // manifest 文件也可以指定缓存, manifest 文件的建议文件扩展名是：".appcache"
  // manifest 文件需要设置 MIME-type="text/cache-manifest", 必须在 web 服务器上进行配置

[cookies]
```

```
// 检测是否支持本地存储
if (typeof(Storage) !== "undefined") {
    // 针对 localStorage/sessionStorage 的代码
} else {
    // 抱歉！不支持 Web Storage ..
}

// localStorage
// 存储 (名称/值对始终存储为字符串)
localStorage.setItem("lastname", "Gates");
// 取回
localStorage.getItem("lastname");
// 删除
localStorage.removeItem("lastname");

// sessionStorage
//

```

```
[manifest]

	: CACHE MANIFEST  在此标题下列出的文件将在首次下载后进行缓存
	: NETWORK         在此标题下列出的文件需要与服务器的连接，且不会被缓存
	：FALLBACK        在此标题下列出的文件规定当页面无法访问时的回退页面(比如 404 页面)

//
CACHE MANIFEST
# 2012-02-21 v1.0.0
/theme.css
/logo.gif
/main.js

NETWORK:
login.asp

# 规定如果无法建立因特网连接, 则用 "offline.html" 替代 /html/ 目录中的所有文件
FALLBACK:
/html/ /offline.html

	: 更新缓存
  # 用户清空浏览器缓存
  # manifest 文件被修改, 应用的缓存只会在其 manifest 文件改变时被更新
  // 更新注释行中的日期和版本号是一种使浏览器重新缓存文件的办法
  # 程序来更新应用缓存
```

### Web Worker

```
[Web Worker]

	: 当在 HTML 页面中执行脚本时，页面是不可响应的，直到脚本已完成
  : Web worker 是运行在后台的 JavaScript, 独立于其他脚本, 不会影响页面的性能
  # worker 无法访问全局和DOM对象
  
// 检测浏览器是否支持
if (typeof(Worker) !== "undefined") {
    // 是的！支持 Web worker！
} else {
    // 抱歉！不支持 Web Worker！
}

// 开始
w = new Worker("workers.js");

// 添加事件监听器 onmessage
w.onmessage = function(event){
  document.getElementById("result").innerHTML = event.data;
};

// 终止
w.terminate();

// workers.js
var i = 0;

function timedCount() {
    i = i + 1;
    // postMessage() , 用于向 HTML 页面传回一段消息
    postMessage(i);
    setTimeout("timedCount()",500);
}

timedCount();
```

```
<!DOCTYPE html>
<html>
<body>

<p>Count numbers: <output id="result"></output></p>
<button onclick="startWorker()">Start Worker</button> 
<button onclick="stopWorker()">Stop Worker</button>
<br><br>

<script>
var w;

function startWorker() {
    if(typeof(Worker) !== "undefined") {
        if(typeof(w) == "undefined") {
            w = new Worker("demo_workers.js");
        }
        w.onmessage = function(event) {
            document.getElementById("result").innerHTML = event.data;
        };
    } else {
        document.getElementById("result").innerHTML = "Sorry! No Web Worker support.";
    }
}

function stopWorker() { 
    w.terminate();
    w = undefined;
}
</script>

</body>
</html>
```

