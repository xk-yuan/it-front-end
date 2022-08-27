

```
[需要配置WEB启动, 解决跨域请求问题]

	: npm install -g http-server

	# 测试根目录下启动
  : http-server -a localhost -p 8001

// https://www.npmjs.com/package/http-server
// https://github.com/indexzero/http-server

[Vue - Axios]

new Vue({
  el: '#app',
  data () {
    return {
      info: null
    }
  },
  mounted () {
    axios
       .get('/static/json_demo.json')
       .then(response => (this.info = response));
  }
})
```

```
[GET请求]

axios
  .get('/static/json_demo.json')
  .then(function (response) {
  	// handle success
  	console.log(response);
  })
  .catch(function (error) {
  	// handle error
  	console.log(error);
  })
  .finally(function () {
  	// always executed
  });

[GET请求 - 并解析]

	: .then(response => (this.info = response.data.sites))

[GET 请求 - 传参]

	# 直接传参, URL 加上参数
	: axios.get('/user?ID=12345')

	// 也可以通过 params 设置参数：
	: axios.get('/user', {
      params: {
        ID: 12345
      }
    })
 
[POST 请求]

	: axios
      .post('/static/json_demo.json')

[POST 请求 - 传参]

	: axios.post('/user', {
      firstName: 'Fred',        // 参数 firstName
      lastName: 'Flintstone'    // 参数 lastName
    })

[并发执行]

function getUserAccount() {
  return axios.get('/user/12345');
}
 
function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
  }));

[axios API]

axios(config)
// 发送 POST 请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
//  GET 请求远程图片
axios({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  responseType:'stream'
})
  .then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
});
axios(url[, config])
// 发送 GET 请求（默认的方法）
axios('/user/12345');
```

```json
[json_demo.json]

{
	name: "www",
	num: 3,
	sites: [{
			name: "v1",
			info: [
				"x1",
				"x2",
				"x3"
			]
		}
	]
}
```

