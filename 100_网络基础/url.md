
URI：Uniform Resource Identifier，即统一资源标志符，用来唯一的标识一个资源。
URL：Uniform Resource Locator，统一资源定位符。即URL可以用来标识一个资源，而且还指明了如何locate这个资源。
URN：Uniform Resource Name，统一资源命名。即通过名字来表示资源的。

URI
这是一个URI：“http://bitpoetry.io/posts/hello.html#intro” 
“http://”是定义如何访问资源的方式。 
“bitpoetry.io/posts/hello.html”是资源存放的位置。 
“#intro”是资源。 
URL:
URL是URI的一种，不仅标识了Web 资源，还指定了操作或者获取方式，同时指出了主要访问机制和网络位置。 
协议名称，主机名称(IP或者域名)、端口号(默认 为80端口)、路径和查询字符串这5个部分。
比如：“http://bitpoetry.io/posts/hello.html” 
URN
URN是URI的一种，用特定命名空间的名字标识资源。使用URN可以在不知道其网络位置及访问方式的情况下讨论资源。 
比如：“bitpoetry.io/posts/hello.html#intro” 







1、在URL中中文字符通常出现在以下两个地方：
(1)、Query String中的参数值，比如http://search.china.alibaba.com/search/offer_search.htm?keywords=中国
(2)、servlet path，比如：http://search.china.alibaba.com/selloffer/中国.html



三、下面我们分别从浏览器和应用服务器来举例说明：
URL：http://localhost:8080/example/中国?name=中国
汉字   编码      二进制表示
中国   UTF-8     0xe4 0xb8 0xad 0xe5 0x9b 0xbd[-28, -72, -83, -27, -101, -67]
中国   GBK       0xd6 0xd0 0xb9 0xfa[-42, -48, -71, -6]
中国   ISO8859-1 0x3f,0x3f[63, 63]信息失去

(一)、浏览器
1、GET方式提交，
浏览器会对URL进行URL encode，然后发送给服务器。
不同的浏览器以及同一浏览器的不同设置，会影响最终URL中PathInfo的编码。对于中文的IE和FIREFOX都是采用GBK编码QueryString。
(1) 对于中文IE,如果在高级选项中选中总以UTF-8发送(默认方式)，则PathInfo是URL Encode是按照UTF-8编码,QueryString是按照GBK编码。
GET /example/%E4%B8%AD%E5%9B%BD?name=%D6%D0%B9%FA
(1) 对于中文IE,如果在高级选项中取消总以UTF-8发送，则PathInfo和QueryString是URL encode按照GBK编码。
GET /example/%D6%D0%B9%FA?name=%D6%D0%B9%FA
(3) 对于中文firefox，则pathInfo和queryString都是URL encode按照GBK编码。
GET /example/%D6%D0%B9%FA?name=%D6%D0%B9%FA

2、 POST提交
        对于POST方式，表单中的参数值对是通过request body发送给服务器，此时浏览器会根据网页的ContentType("text/html; charset=GBK")中指定的编码进行对表单中的数据进行编码，然后发给服务器。
在服务器端的程序中我们可以通过Request.setCharacterEncoding() 设置编码，然后通过request.getParameter获得正确的数据。
解决方案：
1、从最简单，所需代价最小来看，我们对URL以及网页中的编码使用统一的编码对我们来说是比较合适的。
如果不使用统一编码的话，我们就需要在程序中做一些编码转换的事情。这也是我们为什么看到有网络上大量的资料介绍如何对乱码进行处理，其中很多解决方案都只是一时的权宜之计，没有从根本上解决问题。


(二)、Servlet服务器
        Servlet服务器实现的Servlet遇到URL和POST提交的数据中含有%的字符串，它会按照指定的字符集解码。下面两个Servlet方法返回的结果都是经过解码的：
request.getParameter("name"); 
request.getPathInfo();
这里所说的"指定的字符集"是在应用服务器的配置文件中配置。
(1) tomcat服务器
对于tomcat服务器，该文件是server.xml
<Connector port="8080" protocol="HTTP/1.1" 
               maxThreads="150" connectionTimeout="20000" 
               redirectPort="8443" URIEncoding="GBK"/>
URIEncoding告诉服务器servlet解码URL时采用的编码。
<Connector port="8080" ... useBodyEncodingForURI="true" />
useBodyEncodingForURI告诉服务器解码URL时候需要采用request body指定的编码。



参考资料
http://blog.csdn.net/yzhz/article/details/1676796