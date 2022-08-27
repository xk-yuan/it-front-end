
```
[]

	: https://cdn.staticfile.org/vue-resource/1.5.1/vue-resource.min.js

	: <script src="https://cdn.staticfile.org/vue-resource/1.5.1/vue-resource.min.js"></script>

[vue-resource]

	:
```

```
[GET 请求]

<input type="text" @keyup="sendJsonP(keyword)">

//发送get请求
methods: {
  sendJsonP(keyword) {
     this.$http.get('/try/ajax/ajax_info.txt').then(function(res){
       console.log(res.body);
     },function(){
       console.log('error');
     });
  }
}

// this.$http.get('get.php',{params : jsonData}) 格式，第二个参数 jsonData 就是传到后端的数据

[POST]

//发送 post 请求
this.$http.post(
  '/try/ajax/demo_test_post.php',
  {name:"菜鸟教程",url:"http://www.runoob.com"},
  {emulateJSON:true}
).then(function(res){

},function(res){
  console.log(res.status);
});

// emulateJSON 的作用： 如果Web服务器无法处理编码为 application/json 的请求，你可以启用 emulateJSON 选项
```

```html
[案例]

<!DOCTYPE html>
<html>
<body>
<div id="app">
    <h1>Hello App!</h1>
    请输入关键字: <input type="text" v-model="keyword" @keyup="sendJsonP(keyword)">
    <ul>
        <li v-for="r in result">{{r}}</li>
    </ul>
</div>
</body>
</html>

<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://cdn.staticfile.org/vue-resource/1.5.1/vue-resource.min.js"></script>

<script type="text/javascript">
window.onload = function () {
  new Vue({
    el: '#app',
    data: {
      keyword: '',
      result: ''
    },
    methods: {
      sendJsonP(keyword) {
        let url = 'https://www.baidu.com/sugrec?pre=1&p=3&ie=utf-8&json=1&prod=pc&from=pc_web';
        this.$http.jsonp(url, {
          params: {
            wd: keyword
          },
          jsonp: 'cb'// jsonp默认是callback,百度缩写成了cb，所以需要指定下                     }
        }).then(res => {
          if (res.data.g) {
            this.result = res.data.g.map(x => x['q']);
          } else {
            this.result = [];
          }
        });
      }
    }
  });
}
</script>
```

