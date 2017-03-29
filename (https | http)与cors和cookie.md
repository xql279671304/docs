## HTTPS、HTTP和CORS与COOKIE之间的纠缠

### http
    
    http是【超文本传输协议】，客户端到服务端等一系列的运作流程。其中传输的IP协议、可靠性的TCP协议、域名解析的DNS服务。
    http通信使用明文、不验证身份、不能确保完整性！那么就需要升级～～～
    
### https
    
    粗略的理解https就是在http上面加了一层SSL／TLS协议。
    
#### SSL／TLS 握手
    
    进行了四次握手,公匙加密计算量大，会消耗cpu、耗用时间昌长。
    解决方法：每一次对话（session），客户端和服务器端都生成一个"对话密钥"（session key），用它来加密信息。由于"对话密钥"是对称加密，所以运算速度非常快，而服务器公钥只用于加密"对话密钥"本身，这样就减少了加密运算的消耗时间。
    
![SSL/TLS握手](/images/SSL|TLS.png)
    
    
    
### CORS(Cross-origin resource sharing)

    允许浏览器向跨源服务器，发出XMLHttpRequest请求，客服AJAX只能同源实用的限制。
    
*   服务端和浏览器同时支持，一般浏览器都是支持的 ie10以上
*   回应的头部信息应该有 Access-Control-Allow-Origin字段
*   CORS请求默认是不发送cookie和http认证信息的，如果要把cookie发到服务器，服务器要同意 Access-Control-Allow-Credentials：true，同时请求头部也需要添加字段 withCredentials:true
*   需要发送cookie的时候，Access-Control-Allow-Origin就不能设为星号，必须指定明确的、与请求网页一致的域名。同时，Cookie依然遵循同源政策，只有用服务器域名设置的Cookie才会上传，其他域名的Cookie并不会上传，且（跨源）原网页代码中的document.cookie也无法读取服务器域名下的Cookie。
*   CORS与JSONP的使用目的相同，但是比JSONP更强大。
    JSONP只支持GET请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。    

### cookie

    document.cookie = 'token=AAA;domain=域名;path=/'
    