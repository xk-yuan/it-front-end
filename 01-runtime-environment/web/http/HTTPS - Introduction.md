
```
[HTTP + SSL / TLS]

	: www.rfc-editor.org # RFC2246-TLS

```

    Hyper Text Transfer Protocol over SecureSocket Layer , HTTPS ，是以安全为目标的 HTTP 通道，在HTTP的基础上通过传输加密和身份认证保证了传输过程的安全性。

    HTTPS 在HTTP 的基础下加入SSL 层，HTTPS 的安全基础是 SSL，因此加密的详细内容就需要 SSL。 HTTPS 存在不同于HTTP 的默认端口及一个加密/身份验证层（在 HTTP与 TCP 之间）。这个系统提供了身份验证与加密通讯方法。HTTP 加上 TLS/SSL 协议构建的可进行加密传输、身份认证的网络协议，主要通过数字证书、加密算法、非对称密钥等技术完成互联网数据传输加密，实现互联网传输安全保护。基于X.509证书对双方进行身份认证。

    保证数据保密性，数据内容在传输的过程中不会被第三方查看。保证数据完整性，及时发现被第三方篡改的传输内容。保证身份校验安全性，数据到达用户期望的目的地。

    HTTP协议，其数据的明文传送和消息完整性检测的缺乏, 在传输客户端请求和服务端响应时, 唯一的数据完整性检验就是在报文头部包含了本次传输数据的长度, 而对内容是否被篡改不作确认。

### SSL / TLS

![](../imgs/1573083969721-da71bd96-ce69-41d2-b940-5e2f5264a090.png#align=left&display=inline&height=400&originHeight=359&originWidth=669&size=0&status=done&width=746)

![](../imgs/1573084000299-f5006211-1ead-4ea4-9f34-e8123bf04510.png#align=left&display=inline&height=967&originHeight=609&originWidth=470&size=0&status=done&width=746)

    安全套接层 Secure Socket Layer ，SSL , 基于HTTPS下的一个协议加密层，最初是由网景公司（Netscape）研发，后被IETF（The Internet Engineering Task Force - 互联网工程任务组）标准化后写入（RFCRequest For Comments 请求注释）。

    SSL是基于HTTP之下TCP之上的一个协议层，是基于HTTP标准并对TCP传输数据时进行加密，所以HPPTS是HTTP+SSL/TCP的简称。

    SSL更新到3.0时，IETF对SSL3.0进行了标准化，并添加了少数机制(但是几乎和SSL3.0无差异)，标准化后的IETF更名为TLS1.0(Transport Layer Security 安全传输层协议)，可以说TLS就是SSL的新版本3.1。

    TLS/SSL是一种加密通道的规范，其利用对称加密、公私钥不对称加密及其密钥交换算法，CA系统进行加密且可信任的信息传输。SSL由从前的网景公司开发有1,2,3三个版本，但现在只使用版本3。TLS是SSL的标准化后的产物 有1.0 1.1 1.2三个版本 默认使用1.0。
