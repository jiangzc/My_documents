作者：vosamo007   
来源：CSDN   
原文：https://blog.csdn.net/vosamo007/article/details/49684603    

## <a name="t0"></a>1、上网的整个过程

　　假设我们点击了某网页上的一个链接，指向**清华大学院系设置**，其URL是：[http://www.tsinghua.edu.cn/chn/yxsz/index.html](http://www.tsinghua.edu.cn/chn/yxsz/index.html)。我们来分析一下整个过程：

1.  浏览器分析链接指向页面的URL
2.  浏览器向DNS请求解析www.tsinghua.edu.cn的IP地址
3.  DNS系统解析出清华大学服务器的地址是166.111.4.100
4.  浏览器与服务器建立TCP连接
5.  浏览器发出取文件命令：**GET /chn/yxsz/index.html**
6.  服务器www.tsinghua.edu.cn给出响应，把文件index.html返回给浏览器
7.  释放TCP连接
8.  浏览器解析并显示“清华大学院系设置”文件index.html中的内容

## <a name="t1"></a>2、HTTP协议

　　Internet的基本协议是TCP/IP协议，目前广泛使用的FTP、HTTP协议都是基于TCP/IP的，HTTP是Web应用使用最主要的协议。

　　HTTP基于请求响应模型。客户端向服务器发送一个请求，请求头包含请求的方法、URI、协议版本、以及包含请求修饰符、客户端信息和内容的类似MIME的消息结果。服务器则返回一个状态行作为响应，内容包括消息协议的版本、成功或失败编码加上包含服务器信息、实体元信息以及可能的实体内容。

　　HTTP协议是**无状态**的，也就是说同一用户在第二次访问同一台服务器上的页面时，服务器的响应与第一次被访问时相同。

　　HTTP是**无连接**的，虽然HTTP是基于TCP的，但是HTTP本身是无连接的。客户端和服务器的链接是基于一种请求应答模式。及客户端和服务器建立一个链接，客户端提交一个请求，服务器端收到请求后返回一个响应，然后二者就断开链接。

## <a name="t2"></a>3、请求/响应过程

　　把上面的上网过程抽象一下，得到下面的模型： 

<center>![](http://img.my.csdn.net/uploads/201012/22/0_1293016177wCCA.gif)</center> 

<center>请求/响应模型</center>

上面这个模型比较简单，它描述的是HTTP1.0中的请求/响应过程。我们分析一下，整个过程中花费的时间包括：建立TCP三次握手的时间、客户端发送请求的时间、服务器返回响应的时间。 

下图为请求一个万维网文档所需的时间： 

<center>![](http://img.my.csdn.net/uploads/201202/17/0_1329479478KZsm.gif)</center> 

这样一次成功的请求/响应就要花费2*RTT+传输文档的时间，另外还要考虑客户端和服务器为每一次建立TCP连接分配缓存和变量的开销，如果每次请求都这样，显然开销太大。特别是当有很多用户访问同一台服务器时，这种**非持续的连接**会使得服务器负担很重。HTTP1.1通过引入**持续连接**较好的解决了这个问题。

　　所谓**持续连接**就是服务器在发送一次响应后不是立即断开TCP连接，而是在一段时间内仍然保持连接，使同一用户和该服务器可以继续在这条连接上传送后续的请求和响应。持续连接有两种工作方式：**非流水线式**和**流水线式**。

*   非流水线式：客户在收到一个响应后才能发送下一个请求
*   流水线式：客户在收到HTTP的响应报文之前能够接着发送新的请求报文。于是一个接一个的请求到达服务器后，服务器就可以连续的返回响应报文。

## <a name="t3"></a>4、代理服务器

　　代理服务器是一种网络实体，它又称为万维网高速缓存。代理服务器把最近的一些请求和响应暂存在本地磁盘中。若一个网络中使用了代理服务器，该网络中的主机浏览器向因特网的服务器请求服务时，就先和代理服务器建立TCP连接，并向代理服务器发出HTTP请求报文。若代理服务器中已经存放了所请求的对象，则把这个对象放入HTTP响应报文中返回给客户浏览器；否则，代理服务器就代表客户浏览器与因特网上的源点服务器建立TCP连接，并发送HTTP请求报文。源点服务器把所请求的对象放在HTTP响应报文中返回给代理服务器。代理服务器收到这个对象后，先复制在自己的本地存储器中，然后再把这个对象放在HTTP响应报文中，通过已经建立的TCP连接返回给客户浏览器。

## <a name="t4"></a>5、报文

HTTP有两类报文：

*   请求报文：从客户向服务器发送请求报文。
*   响应报文：从服务器到客户的回答。

由于HTTP是面向文本的，因此在报文中的每一个字段都是一些ASCII码串，因而各个字段的长度都是不确定的。HTTP请求报文和响应报文都是由三个部分组成。这两种报文格式的区别就是开始行不同。

*   **开始行**：用于区分是请求报文还是响应报文。在请求报文中的开始行叫做请求行，而在响应报文中的开始行叫做状态行。
*   **首部行**：用来说明浏览器、服务器或报文主体的一些信息。首部可以有好几行，但也可以不使用。
*   **实体主体**：在请求报文中一般都不用这个字段，而在响应报文中也可能没有这个字段。

<center>![](http://img.my.csdn.net/uploads/201202/17/0_1329479399xURu.gif)</center> 

<center>请求报文</center>

<center>![](http://img.my.csdn.net/uploads/201202/17/0_1329479447r8Lz.gif)</center> 

<center>响应报文</center>

请求：

> GET /sample.jsp HTTP/1.1 
> 
>   Accept:image/gif.image/jpeg,_/_ 
> 
>   Accept-Language:zh-cn 
> 
>   Connection:Keep-Alive 
> 
>   Host:localhost 
> 
>   User-Agent:Mozila/4.0(compatible;MSIE5.01;Window NT5.0) 
> 
>   Accept-Encoding:gzip,deflate

上面是一个请求的例子。

## <a name="t5"></a>6、请求方法和状态码

### <a name="t6"></a>请求方法　　

客户端和服务器之间交互会使用不同的方法。下表列出了HTTP请求报文的几种方法：

<div class="table-box"><table>
<thead>
<tr>
  <th>方法（操作）</th>
  <th>意义</th>
</tr>
</thead>
<tbody><tr>
  <td>OPTIOON</td>
  <td>请求一些选项的信息</td>
</tr>
<tr>
  <td>GET</td>
  <td>请求读取由URL所标记的信息</td>
</tr>
<tr>
  <td>HEAD</td>
  <td>请求读取由URL所标记的信息的首部</td>
</tr>
<tr>
  <td>POST</td>
  <td>向服务器提交信息</td>
</tr>
<tr>
  <td>PUT</td>
  <td>在指明的URL下存储一个文档</td>
</tr>
<tr>
  <td>DELETE</td>
  <td>删除指明的URL所标记的资源</td>
</tr>
<tr>
  <td>TRACE</td>
  <td>用来进行环回测试的请求报文</td>
</tr>
<tr>
  <td>CONNECT</td>
  <td>用于代理服务器</td>
</tr>
</tbody></table></div>

### <a name="t7"></a>状态码

状态码都是三位数字的：

*   1xx 表示通知信息，如请求收到或正在进行处理
*   2xx 表示成功，如接受或知道了
*   3xx 表示重定向，如要完成请求还必须采取进一步的行动
*   4xx 表示客户的差错，如请求中有错误的语法或不能完成
*   5xx 表示服务器的差错，如服务器失效无法完成请求

## <a name="t8"></a>参考资料

*   计算机网络（第六版）  谢希仁
*   [Http协议分析](http://www.xuebuyuan.com/1494601.html "Http协议分析")
*   [理解HTTP协议的Request/Response模型](http://blog.sina.com.cn/s/blog_5e98ca2b01018p3j.html)
*   [HTTP深入浅出 http请求](http://www.cnblogs.com/yin-jingyu/archive/2011/08/01/2123548.html) 
