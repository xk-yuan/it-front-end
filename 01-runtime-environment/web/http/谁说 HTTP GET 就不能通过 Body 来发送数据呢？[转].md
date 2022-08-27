当我们被问及 HTTP 的 GET 与 POST 两种请求方式的区别的时候，很多答案是说 GET 的数据须通过 URL 以 Query Parameter 来传送，而 POST 可以通过请求体来发送数据，所以因 URL 的受限，往往 GET 无法发送太多的字符。

这个回答好比在启用了 HTTPS 时，GET 请求 URL 中的参数仍然是明文传输的一样。
GET 果真不能通过 Request Body 来传送数据吗？

非也。

如此想法多半是因循着网页中 form 的 method 属性只有 get 与 post 两种而来。因为把 form 的 method 设置为 post，表单数据会放在 body 中，而 method 为 get(默认值) 时，提交时浏览器会把表单中的字符拼接到 action 的 URL 后作为 query parameter 传送。

![](../imgs/1567587942644-470c5be9-6257-405a-ac5a-41f1f2ffe427.jpeg#align=left&display=inline&height=995&originHeight=640&originWidth=480&size=0&status=done&width=746)


GET vs POST

于是乎就有了这么一种假像：HTTP GET 必须通过 URL 的查询参数来发送数据。

其实 HTTP 规范并未规定说 GET 就不能发送 body 数据，在 RFC GET 中只是说：

> The GET method means retrieve whatever information (in the form of an entity) is identified by the Request-URI.


只是说 GET 意味着通过 URI 来识别资源。

# 测试


我也是本着传统上对 GET 与 POST 区别的误解很多年，今天突然意识到 GET 应该可以使用 body，况且 HTTP 本身是一个纯文本的协议。

没有测试就没有 100% 的发言权，所以做了如下的测试。

在一个 Spring Boot Web 项目中创建的 GET 请求 API：

```
@RestController
public class DemoController {
 
    @RequestMapping(value = "/", method = RequestMethod.GET)
    public String getRequest(@RequestParam("id") String id, @RequestBody String body) {
        return id + ": " + body;
    }
}
```

上而创建的 GET 请求，URL 是 `/?id=something`，然后希望通过 request body 来获得请求数据。

再来一个测试用例，给 GET 请求发送 body 数据：

```
@RunWith(SpringRunner.class)
@WebMvcTest
public class DemoControllerTest {
 
    @Autowired
    private MockMvc mockMvc;
 
    @Test
    public void shouldReturnDefaultMessage() throws Exception {
        this.mockMvc
            .perform(get("/?id=100")
            .content("Hello, Get Body"))
            .andDo(print())
            .andExpect(content().string(is("100: Hello, Get Body")));
    }
}
```

上面的单元测试顺利通过，说明对于 GET 请求我们同样可以使用 Request Body 来发送数据，而且 Spring 的测试框架也支持 GET 发送 body 数据。

再作一个验证，curl 命令, 需要用 -X 指定为 GET 请求，否则 curl 在使用 -d 发送 body 数据时自动切换为 POST 请求：

![](../imgs/1567587942625-c90cdf5c-2511-478c-be22-e76e6ddeb79e.jpeg#align=left&display=inline&height=664&originHeight=664&originWidth=740&size=0&status=done&width=740)

curl

通过 `curl -v` 可以看到详细的请求响应数据，两个请求的 Content-Length 都是 8，即 "Get Body" 的长度，它们确实是在 Request Body 中，服务端接送 GET 来的 body 数据也没有半点问题。

下面是通过 Wireshark 捕获到的数据包的样子：

![](../imgs/1567587942646-6a642b0e-ce91-44a3-a1f5-9abd0464a345.jpeg#align=left&display=inline&height=749&originHeight=749&originWidth=1099&size=0&status=done&width=1099)


Wireshark
# 其他工具的支持情况


如果说通过 Spring 的测试用例以及 curl 命令还有所疑问的话，看上面那张图片就分明的告诉我们是在使用 GET 发送 body 数据的。

但确实有些工具或类库不让我们发送 GET 请求时设置 Body。

## Postman


如著名的 Postman，在选择 GET 时 Body 标签是灰色不可用的：

![](../imgs/1567587942661-92e51f96-84f0-4853-b854-7698ed68644b.jpeg#align=left&display=inline&height=416&originHeight=416&originWidth=766&size=0&status=done&width=766)
Postman

而且从目前最新的 Apache Http Client 4.5 组件，它的 HttpGet 也不支持设置 Request Body, 因为 HttpGet 没有像 HttpPost 那样的 setEntity(entity) 方法。

## OkHttpClient


另一个 OkHttpClient 库也不支持 GET 发送 Request Body，当执行下面的代码时：
```
new Request.Builder()
   .url("http://localhost:8080/?id=100")
   .method("GET", RequestBody.create(MediaType.parse("application/json"), "hello body"))
   .build();
```

直接告诉我:
> java.lang.IllegalArgumentException: method GET must not have a request body

## 
## AsyncHttpClient
最后再试一个 AsyncHttpClient 库：
```
Dsl.asyncHttpClient()
   .prepareGet("http://localhost:8080/?id=100")
   .setBody("Get Body")
   .execute()
   .toCompletableFuture()
   .thenAccept(System.out::println).join();
```

输出 "100: Get Body", 证明 AsyncHttpClient 是可以 GET 时发送 Body 数据的。
# 小结一下


Apache Http Client 和 OkHttpClient 都不支持 GET 请求发送 Body 数据，而 AsyncHttpClient 是可以的。

那么回过头来想想为什么 HTTP 并未规定不可以 GET 中发送 Body 内容，但却不少知名的工具不能用 GET 发送 Body 数据，所以大致的讲我们仍然不推荐使用 GET 携带 Body 内容，还有可能某些应用服务器也会忽略掉 GET 的 Body 数据（???，猜的）。

我想更主要是 GET 被设计来用 URI 来识别资源，如果让它的请求体中携带数据，那么通常的缓存服务便失效了，URI 不能作为缓存的 Key。

但另一方面，如果仅仅是为了读取资源，而需要使用 Body 发送一大批数据时，改用 POST 请求却与 RESTFul 的 POST 语义不相符。这时候或许可以 GET + BODY, 但是不能对该请求以 URI 作为 Key 进行缓存了。
