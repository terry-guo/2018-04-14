# 一.网络相关基本概念

##1. 基本概念

客户端（Client）：移动应用（iOS、android等应用）
服务器（Server）：为客户端提供服务、提供数据、提供资源的机器
请求（Request）：客户端向服务器索取数据的一种行为
响应（Response）：服务器对客户端的请求做出的反应，一般指返回数据给客户端

##2. 服务器介绍和分类

（1）简单介绍
    服务器也是电脑，只不过是比我们的电脑配置更高的电脑，并且24小时不断电，不关机的计算机
    服务器是专门用于存储数据电脑， 访问者可以访问服务器获得服务器上存储的资源
    服务器其实就是一台"提供了某种服务功能"的电脑

（2）服务器的分类
    按照软件开发阶段来分，服务器可以大致分为2种
    01 远程服务器
        别名：外网服务器、正式服务器
        使用阶段：应用上线后使用的服务器
        使用人群：供全体用户使用
        速度：取决于服务器的性能、用户的网速

​    02 本地服务器
        别名：内网服务器、测试服务器
        使用阶段：应用处于开发、测试阶段使用的服务器
        使用人群：仅供公司内部的开发人员、测试人员使用
        速度：由于是局域网，所以速度飞快，有助于提高开发测试效率

​    按服务器类型分:
        文件服务器
        数据库服务器
        邮件服务器
        Web 服务器等；

​    按软件类型分:
        Apache服务器
        IIS服务器
        Tomcat服务器
        Nginx 服务器
        Node服务器等

​    按操作系统分:
        Windows服务器
        Linux服务器等；

###3 访问网页原理

​	1.访问网页时是有真实的、物理的文件传输的
	2.网页不是一个文件，而是一堆文件组成的
	3.我们之所以平常感觉第二次访问比第一次访问快的原因就是，第一次访问时已经将所有文件缓存到了本地

###4 浏览器请求数据的过程

​	1.按下回车时浏览器根据输入的URL地址发送请求报文给服务器
	2.服务器接收到请求报文，会对请求报文进行处理
	3.服务器将处理完的结果通过响应报文返回给浏览器
	4.浏览器解析服务器返回的结果，将结果显示出来

###5 常见的服务器软件

​	文件服务器软件：
   		 Server-U、FileZilla、VsFTP等；
	数据库服务器软件：
  	  	Oracle、MySQL、PostgreSQL、MSSQL等；
	邮件服务器软件：
 		   Postfix、Sendmail等；
	HTTP 服务器软件：
 	 	  Apache、IIS、Tomcat、Nginx、NodeJS等；



# 二.Ajax

### 1.什么是Ajax?

​	AJAX = 异步 JavaScript 和 XML。

​	AJAX 是一种用于创建快速动态网页的技术。

​	通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

​	ajax请求的种类一共有get , post ,  put ,  head，options，trace , delete , patch，目前常用的有get方法和post方法。

#### get方法和post方法比较

01 安全性

```
GET请求请求的参数直接拼接在URL后面发送给服务器，可以通过浏览记录来查看，另外如果黑客攻破了服务器拿到服务器的访问日志，那么所有的访问记录都会被暴露。
POST请求的请求参数存放在请求体中传递，相对安全。
```

02 大小限制

```
get请求：
因为"特定的浏览器及服务器对请求的URL长度有限制"，而get请求的参数又全部拼接在URL后面处理。
所以在使用get方法网络请求的时候，对参数的大小有限制。

post请求：
因为POST不是通过URL提交数据,所以POST是没有大小限制。
HTTP协议规范也没有进行大小限制，起限制作用的是服务器的处理程序的处理能力。
```

03 请求体

```
get请求因此所有的参数都拼接在请求路径后面，所以没有请求体
post请求把参数全部都放在请求体中传递。
```

####ajax请求的基本过程：

1.创建异步对象

~~~
if(window.XMLHttpRequest){
    var xhr = new XMLHttpRequest();
}else{
    var xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
~~~

2.get 方法设置URL，发送请求

~~~
xhr.open("get", url, true);
xhr.send();
~~~

3.post 方法设置URL，发送请求

~~~
xhr.open("POST",url,true);
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send("user=abc&password=123"); //这里设置请求的参数
~~~

4.监听状态，处理返回结果

~~~
xhr.onreadystatechange = function () {
    // 5.处理返回结果
    if(xhr.readyState == 4){
      
        if(xhr.status >= 200 &&
            xhr.status < 300 ||
            xhr.status == 304){
            // 这里执行请求成功之后的回调
        }else{
            error(xhr.status); //请求失败的回调
        }
    }
}
~~~

onreadystatechange的几种状态：
	（1）请求未初始化 - 0
	（2）服务器连接已经建立 - 1
	（3）请求已经接收 -2
	（4）请求处理中 -3
	（5）请求已经完成，且响应已经就绪 -4

处理请求结果
	（1）当请求完成的时候再进行处理，即readyState == 4
	（2）通过响应码判断只有请求成功的时候才进行处理，即响应码>=200,<300或者是=304（缓存）
	（3）拿到服务器返回的响应体：response.Text



###2.请求和响应相关信息

```
url:同一资源定位符，客户端通过URL地址找到服务器端
网络请求的两个部分：请求和响应
请求：（请求头 + 请求体）客户端向服务器索要数据的行为
响应：（响应头 + 响应体）服务器向客户端返回数据的行为

请求的组成部分
    （1）请求头（存放的是对客户端以及请求本身的描述信息）
    （2）请求体（如果是POST请求，则存放发送给服务器的参数）
响应的组成部分
    （1）响应头（存放的是服务器端以及已经响应本身的描述信息）
    （2）响应体（返回给客户端的具体数据）
    （3）响应行（响应状态码 + 原因短语）

请求头可能包含的信息：
    User-Agent：浏览器的具体类型　　如：User-Agent：Mozilla/5.0 (Windows NT 6.1; rv:17.0) Gecko/20100101 Firefox/17.0
    Accept：浏览器支持哪些数据类型　　如：Accept: text/html,application/xhtml+xml,application/xml;q=0.9;
    Accept-Charset：浏览器采用的是哪种编码　　如：Accept-Charset: ISO-8859-1
    Accept-Encoding：浏览器支持解码的数据压缩格式　　如：Accept-Encoding: gzip, deflate
    Accept-Language：浏览器的语言环境　　如：Accept-Language zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3
    Host：请求的主机名，允许多个域名同处一个IP地址，即虚拟主机。Host:www.520it.com
    Connection：表示是否需要持久连接。Keep-Alive/close，HTTP1.1默认是持久连接，它可以利用持久连接的优点，当页面包含多个元素时（例如Applet，图片），显著地减少下载所需要的时间。要实现这一点，Servlet需要在应答中发送一个Content-Length头，最简单的实现方法是：先把内容写入ByteArrayOutputStream，然后在正式写出内容之前计算它的大小。如：Connection: Keep-Alive
    Content-Length：表示请求消息正文的长度。对于POST请求来说Content-Length必须出现。
    Content-Type：WEB服务器告诉浏览器自己响应的对象的类型和字符集。例如：Content-Type: text/html; charset='gb2312'
    Content-Encoding：WEB服务器表明自己使用了什么压缩方法（gzip，deflate）压缩响应中的对象。例如：Content-Encoding：gzip
    Content-Language：WEB服务器告诉浏览器自己响应的对象的语言。
    Cookie：最常用的请求头，浏览器每次都会将cookie发送到服务器上，允许服务器在客户端存储少量数据。
    Referer：包含一个URL，用户从该URL代表的页面出发访问当前请求的页面。服务器能知道你是从哪个页面过来的。Referer: http://www.baidu.com/


响应头可能包含的信息：
    Server:WEB 服务器表明自己是什么软件及版本等信息。例如：Server：Apache/2.0.61 (Unix)
    Accept-Ranges:WEB服务器表明自己是否接受获取其某个实体的一部分（比如文件的一部分）的请求。bytes：表示接受，none：表示不接受
    Content-Type:WEB 服务器告诉浏览器自己响应的对象的类型。例如：Content-Type：application/xml
    Etag:就是一个对象（比如URL）的标志值，就一个对象而言，比如一个html文件，如果被修改了，其Etag也会别修改，所以，ETag的作用跟Last-Modified的作用差不多，主要供WEB服务器判断一个对象是否改变了。比如前一次请求某个html文件时，获得了其 ETag，当这次又请求这个文件时，浏览器就会把先前获得ETag值发送给WEB服务器，然后WEB服务器会把这个ETag跟该文件的当前ETag进行对比，然后就知道这个文件有没有改变了。
    Allow:服务器支持哪些请求方法（如GET、POST等）
    Location:表示客户应当到哪里去提取文档，用于将接收端定位到资源的位置（URL）上。Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法，该方法同时设置状态代码为302。
    Content-Base:解析主体中的相对URL时使用的基础URL。
    Content-Encoding:WEB服务器表明自己使用了什么压缩方法（gzip，deflate）压缩响应中的对象。例如：Content-Encoding：gzip
    Content-Language:WEB 服务器告诉浏览器理解主体时最适宜使用的自然语言。
    Content-Length:WEB服务器告诉浏览器自己响应的对象的长度或尺寸，例如：Content-Length: 26012
    Content-Location:资源实际所处的位置。
    Content-MD5:主体的MD5校验和。
    Content-Range:实体头用于指定整个实体中的一部分的插入位置，他也指示了整个实体的长度。在服务器向客户返回一个部分响应，它必须描述响应覆盖的范围和整个实体长度。一般格式： Content-Range:bytes-unitSPfirst-byte-pos-last-byte-pos/entity-legth。例如，传送头500个字节次字段的形式：Content-Range:bytes0- 499/1234如果一个http消息包含此节（例如，对范围请求的响应或对一系列范围的重叠请求），Content-Range表示传送的范围，Content-Length表示实际传送的字节数。
    Expires:WEB服务器表明该实体将在什么时候过期，对于过期了的对象，只有在跟WEB服务器验证了其有效性后，才能用来响应客户请求。是 HTTP/1.0 的头部。例如：Expires：Sat, 23 May 2009 10:02:12 GMT
    Last-Modified:WEB服务器认为对象的最后修改时间，比如文件的最后修改时间，动态页面的最后产生时间等等。例如：Last-Modified：Tue, 06 May 2008 02:42:43 GMT
```